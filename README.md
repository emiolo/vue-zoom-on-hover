# eMiolo - Vue Zoom on Hover

## Install

```sh
npm install --save https://github.com/emiolo/vue-zoom-on-hover
```

## Usage

```javascript
import ZoomOnHover from '@emiolo/vue-zoom-on-hover/src/ZoomOnHover' // The path is needed because we don't have a build system yet

export default {
  components: { ZoomOnHover},
}
```

```html
<ZoomOnHover src="https://picsum.photos/1920/1080" scale-factor="3"></ZoomOnHover>
```

## To Do

* [ ] Add build system
* [ ] Publish to NPM
* [ ] Write better documentation
