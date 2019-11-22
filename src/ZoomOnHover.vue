<template>
  <div class="vue-zoom-on-hover" v-bind:style="style">
    <img v-bind:src="src" v-bind:key="src + scaleFactor" />
  </div>
</template>

<script>
export default {
  name: 'ZoomOnHover',
  props: {
    src: {
      type: String,
      required: true,
    },
    scaleFactor: {
      type: Number,
      default: 2,
    },
  },
  data: () => ({
    position: {
      x: 50,
      y: 50,
    },
  }),
  computed: {
    style() {
      const {scaleFactor, position} = this
      return `
        --hover-scale: ${scaleFactor};
        --hover-pos-x: ${position.x}%;
        --hover-pos-y: ${position.y}%;
      `
    },
  },
  mounted() {
    this.$el.addEventListener('mousemove', this.onMouseMove)
    this.$el.addEventListener('mouseout', this.onMouseOut)
  },
  methods: {
    limits(value) {
      if (value < 0) return 0
      if (value > 100) return 100
      return value.toFixed(2)
    },
    onMouseMove(event) {
      const {target, clientX, clientY} = event
      const {clientWidth, clientHeight} = target
      const x = this.limits(clientX / clientWidth * 100)
      const y = this.limits(clientY / clientHeight * 100)
      this.position = {x, y}
    },
    onMouseOut() {
      this.position = {
        x: 50,
        y: 50,
      }
    },
  }
}
</script>

<style scoped>
.vue-zoom-on-hover {
  --hover-scale: 3;
  --hover-pos-x: 50%;
  --hover-pos-y: 50%;
  position: relative;
  overflow: hidden;
}
.vue-zoom-on-hover img {
  height: 100%;
  width: 100%;
  object-fit: cover;
  position: absolute;
  transition: transform 0.5s, transform-origin 0.5s;
  transform: scale(1) translate(0, 0);
  transform-origin: var(--hover-pos-x) var(--hover-pos-y);
}
.vue-zoom-on-hover:hover img {
  transform: scale(var(--hover-scale));
  transition: transform 0.2s, transform-origin 0s;
}
</style>
