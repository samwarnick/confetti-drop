# `confetti-drop`

A web component for making stuff fall.

[Demo](https://samwarnick.github.io/confetti-drop/demo.html)

## Installation

Via [`npm`](https://www.npmjs.com/package/@samwarnick/confetti-drop) or download [`confetti-drop.js`](./confetti-drop.js) directly for use in your project.

```bash
npm install @samwarnick/confetti-drop
```

## Usage

```html
<confetti-drop autostart shapes="s,a,m" colors="crimson,#2364AA,--color" spawn-rate="6" fall-time="8"></confetti-drop>
```

### Attributes

- `autostart`
  - Add to start the animation automatically when the element is attached to the DOM. Leave off to manually call `start()`.
- `colors` default: `"#2364AA,#3DA5D9,#EA7317,#FEC601"`
  - Comma separated list. Each particle will be assigned a random color from this list.
  - Colors that start with `--` will be wrapped in `var()`.
- `default-duration` default: `null`
    - How many seconds particles will be generated for. Generation will be stopped after this time. Leave as `null` to generate particles forever.
- `fall-time` default: `5`
    - How many seconds it takes a particle to move 1000px. Higher is slower.
- `shapes` default: `"square"`
  - Comma separated list. Each particle will be assigned a random shape from this list. 
  - Available shapes: `square`, characters, or emoji.
- `spawn-rate` default: `8`
    - How many particles per second are created.

### Methods

- `start(duration = null)`
  - Starts particle generation.
  - Pass in an optional duration in seconds to override the `duration` attribute.
- `stop()`
  - Stops particle generation. Existing particles will continue to fall.
- `burst()`
  - Increases the rate of particle generation for a short time and spawns them closer together.

## Handling `prefers-reduced-motion`

`confetti-drop` will not respect `autostart` if reduced motion is enabled. Other than that, it is up to you to handle reduced motion yourself and avoid calling `start()`.

Internally, `confetti-drop` uses the [`window.matchMedia` API](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) to check for this preference. You can check the user's preference easily with the following code:

```js
window.matchMedia(`(prefers-reduced-motion: reduce)`).matches // returns `true` or `false`
```

## Changelog

- `v1.0.0`
  - Initial release
- `v1.0.1`
  - Particles were being destroyed too quickly when used in a smaller container.
- `v1.1.0`
  - Use container size to correctly position particles.
    - Will now correctly cover entire container and not just 100vh.
  - Fall time is now a consistent time to move 1000px and not 100vh. So partcles will not be faster or slower depending on container height.
  - Fixed a bug where spamming `burst()` would unexpectedly get component stuck running.
