# GridLab / Pixel Lab

A pixel, vector and motion studio that runs entirely in the browser. Drop an image, a GIF, a video or a whole folder and get pixel art back as SVG, PNG, sprite sheets, GIF, WebM or animated SVG, with 15 dither modes, palette control, cleanup, texture grammars, ASCII renderers, an FX lab and optional AI masks. One HTML file, no build step, no server, nothing uploaded.

**Use it here: [getillustrations.com/tools/pixel-lab](https://getillustrations.com/tools/pixel-lab)**, where it runs as *Pixel Lab* inside the GetIllustrations site, with a guide, screens and FAQ. The same file is served standalone from this repo at [ramywafaa.github.io/gridlab](https://ramywafaa.github.io/gridlab/).

Made by [GetIllustrations](https://getillustrations.com), the illustration and icon library. MIT licensed.

---

## Quick start

1. Open [the tool](https://getillustrations.com/tools/pixel-lab/app) (or `index.html` from this repo in any modern browser).
2. Drop a PNG, JPG, WebP, SVG, GIF or MP4/WebM/MOV on the canvas, or paste from the clipboard. Folders and ZIP archives work too.
3. Pick a quality preset and a pixel budget, or leave *Auto recommended*. Auto tune reads the image and sets sampling, palette size and dither for a first pass.
4. Adjust palette, dither, cleanup. Every change re-renders the preview.
5. Export: **SVG** (master or optimised), **PNG** (1x to 16x), sprite sheet ZIP, GIF, WebM, animated SVG, ASCII text, or the settings and palette as JSON.

Keyboard: `Ctrl/Cmd+Enter` convert · `Ctrl/Cmd+S` download optimised SVG · `Ctrl/Cmd+K` search controls · `Ctrl/Cmd+Z` / `Ctrl/Cmd+Shift+Z` undo / redo settings · `G` grid overlay · `1` `2` `3` preview tabs · `F` hide both panels · hold `Space` and drag to pan · `Shift+0` 100% · `Shift+1` fit.

## Running it yourself

There is nothing to install. Clone the repo and open `index.html`, or host the file anywhere static. The only network request the tool ever makes is the optional AI model (see *AI semantic zones* below); everything else is local.

```
git clone https://github.com/RamyWafaa/gridlab.git
open gridlab/index.html
```

Settings, saved presets, module state and collection fingerprints live in `localStorage`. Export them as JSON from module 09 if you want to move or share them.

## The 22 modules

The left rail is a list of modules. *Essentials* shows the first five; *All* shows everything; each module has a switch, and an off module costs nothing.

| # | Module | What it does |
|---|---|---|
| 01 | Source | Files, folders, ZIP and media input: images, GIF and video frames, clipboard paste, multi-file queues. |
| 02 | Auto setup | Quality presets, pixel budget (25K to 400K cells), auto tune, and the 30-recipe style deck with Smart Match, Compare 4 and 3 Variants. |
| 03 | Resolution and framing | Grid width and height, source pixels per cell, resolution multiplier, aspect lock, contain / cover / stretch. |
| 04 | Sampling and edges | Area average, edge-aware area sample, smooth canvas sample or nearest neighbour; edge detection map and edge protection. |
| 05 | Colour system | Auto-extracted palette, style presets (Space Warm, Space Cool, Ancient Stone, Forest Ember, Coral Night, Mono Dramatic, GetIllustrations Brand) or a custom list; colour count, minimum separation, locked colours, background detection. |
| 06 | Dither | 15 modes (below), strength, serpentine diffusion, pattern scale. |
| 07 | Cleanup | Neighbour cleanup passes, isolation threshold, island removal by fragment size, stair-step regularisation, edge protection. |
| 08 | SVG and PNG export | Master SVG (one rect per cell), optimised SVG (same-colour cells merged into larger rectangles), pixel forms (square, inset tile, diamond, beveled, dot), PNG at 1x to 16x, mask PNG, ZIP package, copy SVG to clipboard. |
| 09 | Saved settings | Named presets, JSON import and export, undo / redo history. |
| 10 | Sharp Pixel style grammar | A texture grammar applied per cell or per region: engraving, crosshatch, weave, facet, dissolve, cluster and classic modes. |
| 11 | Bulk automation | Batch conversion of a queue or folder with one preset; ZIP output with SVG, PNG and JSON per image. |
| 12 | Folder rules | Per-folder automatic preset routing for bulk runs. |
| 13 | Sprite sheet | Packs frames into an atlas with configurable tile size, columns and padding; ZIP with PNG sheet plus JSON frame metadata. |
| 14 | GIF / Video | Frame extraction from GIF and video sources; GIF and WebM export at chosen frame rate, duration, scale and bitrate; time-varying FX per frame; animated SVG export. |
| 15 | Adaptive reconstruction | Variable detail density: keeps fine cells where the edge map says the image needs them, simplifies elsewhere. |
| 16 | Perceptual tone shaping | Shadow, mid and highlight shaping before quantisation. |
| 17 | AI semantic zones + mask | SegFormer segmentation in the browser (Transformers.js), heuristic fallback, painted masks; dither, palette and FX can be restricted per zone. |
| 18 | Pattern lab | Custom 4x4 and 8x8 ordered-dither tiles. |
| 19 | Collection style system | Fingerprints up to 10 example images (palette, density, contrast) and keeps a set consistent; recommends presets by score. |
| 20 | GPU 4K preview | WebGL render of the result at up to 4K for print-size PNG export. |
| 21 | FX lab | Post effects on the pixel output: mono and CMYK halftone, seven ASCII renderers plus Braille and Matrix, VHS / digital / chromatic glitch, crosshatch, line art, engraving, stipple, Kuwahara, CRT curvature, bloom, chromatic aberration, film grain; stackable, randomisable, exportable as PNG, GIF, WebM or animated SVG. |
| 22 | Procedural texture overlay | A non-destructive texture layer over the output. |

### Dither modes

Error diffusion: Floyd-Steinberg, Atkinson, Stucki, Burkes, Sierra, Sierra Lite, Jarvis-Judice-Ninke. Threshold and ordered: random threshold, blue-noise style, clustered dot, checker transition, sparse transition, Bayer 2x2, Bayer 4x4, Bayer 8x8. *None* gives the cleanest flat quantisation. Ordered modes dither between the two closest palette colours rather than lightening or darkening a single one.

### Export formats

| Format | Details |
|---|---|
| Master SVG | One `<rect>` per cell, `shape-rendering="crispEdges"`, metadata block. Every pixel is editable in Figma, Illustrator or Inkscape. |
| Optimised SVG | Runs of same-colour cells merged into larger rectangles per colour group. Typically 70 to 90% smaller than the master. |
| PNG | 1x, 2x, 4x, 8x, 16x; transparent or flattened background; a separate mask PNG. |
| Sprite sheet ZIP | Packed PNG atlas plus a JSON file describing every frame's position and size. |
| GIF | In-page LZW encoder (GIF89a); global palette derived from the output palette plus the FX paper, ink and brand colours. |
| WebM | `MediaRecorder` capture of the FX cycle at your frame rate and bitrate. |
| Animated SVG | Baked frames of the FX cycle inside one SVG with CSS keyframes; plays anywhere an SVG does. |
| ASCII text | Plain text from any of the ASCII renderers. |
| Settings / palette JSON | Every control value, reproducible; palettes as hex lists. |
| ZIP package | Master SVG + optimised SVG + PNG + settings in one archive. |

## Technical details

**Architecture.** A single HTML file: two `<style>` blocks and three `<script>` blocks, all plain ES2020, no framework, no bundler. The scripts are IIFEs; the only global they create is `window.GridLabStyleAPI` (the style deck's preset API: `presets`, `loadPreset`, `recommendPresets`, `cyclePresets`, `createVariants`, `fillFolderRules`, `currentImageInfo`, `presetScore`, `installBuiltins`).

**Pipeline** (`convert()`): sample the source into a logical grid (area average by default, edge-aware and nearest variants) → edge map → palette (auto extraction, preset or custom, with minimum separation) → quantise with the chosen dither → cleanup passes (isolation, islands, stair-steps, edge protection) → optional adaptive reconstruction, tone shaping, zones and grammar → SVG builders (master and optimised) → previews. The pipeline yields to the UI between stages with `requestAnimationFrame`, so the page stays responsive on large grids; heavy per-cell loops run on typed arrays.

**Palette extraction** builds a colour histogram (top 4,096 entries), converts to CIELAB and seeds centres farthest-first, each candidate scored by its Lab distance from the chosen set times log2 of its frequency, so rare but distinct colours survive and the palette never collapses into near-duplicates. Matching uses a per-colour cache and a two-nearest cache for the ordered modes.

**SVG optimiser.** Cells are grouped by colour, then merged into maximal same-colour rectangles; the master keeps one rect per cell for editability.

**Sprite packer** lays frames out on a fixed-column grid with padding and writes both the atlas PNG and a JSON frame table. The ZIP writer is in-page (stored entries with CRC-32).

**GIF encoder** is an in-page LZW GIF89a writer with a global colour table built from the output palette. **WebM** goes through `MediaRecorder` on an offscreen canvas.

**FX lab and GPU preview** render through WebGL (2D canvas fallback for the ASCII and halftone renderers). ASCII renderers map cell luminance to character ramps; Braille packs 2x4 dot cells; Matrix draws digit rain.

**AI semantic zones.** On demand, the tool dynamically imports `@huggingface/transformers` 3.7.2 from jsDelivr (with esm.sh as a fallback) and runs an `image-segmentation` pipeline with `Xenova/segformer-b0-finetuned-ade-512-512` (default, about 40 MB, `q8` on WASM or `fp16` on WebGPU) or `onnx-community/segformer-b3-finetuned-ade-512-512-ONNX`. Weights come from Hugging Face and are cached by the browser. If the model cannot load, a heuristic segmenter takes over. Nothing else ever leaves the machine.

**Storage.** `localStorage` keys: `svgPixelConverter.v4.*` (settings, collapse state, presets) and `gridlab.v10.modules` (which modules are on).

**Browser support.** Current Chrome, Edge, Firefox and Safari. WebGPU acceleration for the AI model where available; WebGL for the GPU preview and FX; `MediaRecorder` for WebM. On a phone the layout stacks and the tool stays usable, but a laptop is the intended home.

## Hosting inside a site

The GetIllustrations integration keeps this file as the source of truth. Its build (`scripts/pixel-lab/` in the site repo) scopes every CSS selector under a wrapper class, re-colours the stylesheet to the site's studio palette by hue mapping, and mounts the body markup inside the site layout with the three scripts unchanged except for four one-line edits that keep the panel toggle, collapse memory and space-to-pan shortcut inside the wrapper. If you embed the tool in your own page, do the same: scope the CSS, keep the scripts verbatim, and serve it with a CSP that allows `wasm-unsafe-eval` and the Hugging Face hosts if you want the AI mask.

## Licence

MIT. Copyright 2026 Vectopus FZ-LLC / GetIllustrations. Artwork you convert stays yours; pixel-art versions of GetIllustrations packs follow the licence of the pack.
