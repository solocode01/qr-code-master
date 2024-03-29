A no-framework, no-dependencies, customizable, animate-able, SVG-based `<qr-code>` HTML element. It's just a single, self-contained [Web Component](https://developer.mozilla.org/en-US/docs/Web/Web_Components).

# Usage

Import `<qr-code>` using your build system or framework (e.g. `npm install @solocode01/qr-code`), or use the standalone script in your HTML `<head>` element:

```html
<script src="https://unpkg.com/@solocode01/qr-code@1.0.2/dist/qr-code.js"></script>
```

Then use the component anywhere in your HTML `<body>` element:

```html
<qr-code contents="https://solocode01.com"></qr-code>
```

## Full Example

Here's an example in pure HTML using most features:

```html
<qr-code
  id="qr1"
  contents="https://solocode01.com/"
  module-color="#1c7d43"
  position-ring-color="#13532d"
  position-center-color="#70c559"
  mask-x-to-y-ratio="1.2"
  style="
    width: 200px;
    height: 200px;
    margin: 2em auto;
    background-color: #fff;
  "
>
  <img src="assets/1.2-x-to-y-ratio-icon.svg" slot="icon" />
</qr-code>

<script>
  document.getElementById("qr1").addEventListener("codeRendered", () => {
    document.getElementById("qr1").animateQRCode("MaterializeIn");
  });
</script>
```

## Animations

Animate in, animate on user interactions like URL hits or detected payments, and/or animate out when the QR code interaction is complete.

Several preset animations are available, simply run them with the element's `animateQRCode` method:

```js
document.getElementById("qr1").animateQRCode("RadialRipple");
```

Available built-in presets:

- `FadeInTopDown`
- `FadeInCenterOut`
- `MaterializeIn`
- `RadialRipple`
- `RadialRippleIn`

You can also design your own custom animations! Just pass a function to the `qr-code`'s `animateQRCode` method, e.g.:

```js
document
  .getElementById("qr1")
  .animateQRCode((targets, _x, _y, _count, entity) => ({
    targets,
    from: entity === "module" ? Math.random() * 200 : 200,
    duration: 500,
    easing: "cubic-bezier(.5,0,1,1)",
    web: { opacity: [1, 0], scale: [1, 1.1, 0.5] },
  }));
```

The [built-in presets use this API internally](src/components/qr-code/animations.ts), so review those for guidance and inspiration. Pull request for new presets are welcome!

## Animation Previewer

The **animation previewer makes fine-tuning animations much easier**: try it by cloning this repo and running the live-reloading package script:

```
git clone https://github.com/solocode01/qr-code.git
cd qr-code
npm ci
npm start
```

Then work on your animation in `src/index.html` using the animation previewer (at the bottom right of the window) to test the last-run animation at various speeds, scrub through it manually, or play it in reverse.

## Production build

Disable the `just-animate` player in [`src/components/qr-code/qr-code.tsx`](src/components/qr-code/qr-code.tsx), then build:

```bash
npm run build
```

You can test the built component by pointing the script in [`index.html`](index.html) to `dist/qr-code.js` and opening the page via the local filesystem.
