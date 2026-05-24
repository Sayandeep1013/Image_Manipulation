# SVG Dither Filter

This copy adds a centered preview window around the canvas so the rendered output stays contained inside the stage.

A zero-dependency, single-file tool that turns an uploaded image or video into a
shape-based dither using your own SVGs — then exports the result as a ready-to-use
**hero background**.

No build step, no install. Open `index.html` in a browser and go.

![status](https://img.shields.io/badge/build-none%20required-success)
![license](https://img.shields.io/badge/license-MIT-blue)

## Demo

![Demo of the SVG dither filter applied to a video](assets/demo.gif)

## Features

- **Image & video input** — drag in a still or a video; video is filtered live, frame by frame.
- **Aspect ratio** — keep the original or center-crop to **1:1**.
- **Grid resolution** — 4–160 cells across; rows derived from the aspect ratio.
- **Background colour** — solid fill behind the shapes.
- **7 SVG shapes** — upload up to seven SVGs, one per tone, each with its own colour.
  Empty slots fall back to a built-in circle.
- **7 tone states** — pixel brightness is bucketed shadow → highlight, each bucket
  drawing its slot's shape and colour.
- **Invert** — flip the tone → shape mapping.
- **Shape mode** — *Per-tone* uses all seven shapes, or *Single* uses one chosen
  shape for every cell (scaled by brightness).
- **Shape scale (midtone min → max)** — per-cell size interpolates with brightness.
- **Pixel rotation** — global angle snapped to 90°, plus optional random 90° per cell.
- **Hero export** — emit a standalone HTML hero page, or copy a JSON config for a
  React component.

## Quick start

```sh
# clone, then just open the file — no server needed
open index.html        # macOS
# or double-click index.html in any file manager
```

## Using the tool

1. **Source** — upload an image or video; pick **Original** or **1 : 1**.
2. **Grid** — set resolution and background colour.
3. **Tone mapping** — toggle invert; choose *Per-tone* or *Single* shape mode.
4. **Shape scale** — set min/max size driven by midtone brightness.
5. **Pixel rotation** — pick a 90° angle, optionally randomise per cell.
6. **Shapes** — upload SVGs into slots 1 (shadow) → 7 (highlight) and recolour each.

## Exporting a hero background

### Standalone HTML

1. Tune the look (tune with a still — the dither settings transfer to video 1:1).
2. Enter your **hero video URL** in the export field.
3. Click **Download HTML hero** → produces `dither-hero.html`.

The exported file is fully self-contained: a full-viewport `<section>` with the
dither rendered onto a background `<canvas>`, your SVGs inlined, baked settings,
and a sample headline/CTA layer (`mix-blend-mode: difference` keeps text legible
over any tone). Rendering pauses off-screen via `IntersectionObserver`. Edit the
`<h1>`/`<p>` for your real content.

### React component

Click **Copy config for React hero** to copy a JSON blob (settings + embedded
SVGs). Feed that to your `<DitherHero>` component / generator of choice.

## Caveats

- **Video & CORS** — the canvas reads pixel data, so the video must be same-origin
  or served with permissive CORS headers, otherwise the canvas is tainted and the
  filter cannot read it.
- **SVG recolouring** — colour is applied by overriding `fill`. SVGs whose shape is
  defined purely by `stroke` won't pick up the slot colour.
- **Performance** — dithering video at a high grid is GPU/CPU heavy. For hero use,
  prefer a short muted loop and a moderate grid.

## Browser support

Any modern evergreen browser (Chrome, Edge, Firefox, Safari). Uses Canvas 2D,
`DOMParser`, Blob URLs, and `IntersectionObserver` — no polyfills included.

## Project structure

```
.
├── index.html   # the entire tool — UI, dither engine, and exporters
├── assets/      # demo media (mp4 + gif preview)
├── README.md
└── LICENSE
```

## Credits

Original idea by [antoncreations](https://www.instagram.com/antoncreations/).

## License

[MIT](LICENSE) © MG Productions
