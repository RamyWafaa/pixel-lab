# Module reference

Companion to the README's module table. Numbers match the left rail.

## 01 Source
Accepts PNG, JPG, WebP, SVG (rasterised at import), GIF (frames extracted), MP4 / WebM / MOV (frames sampled), folders and ZIP archives, and clipboard paste. Multiple files form a queue; the batch UI steps through them. *Auto convert after changes* re-runs the pipeline on every control change.

## 02 Auto setup
Quality presets (draft, balanced, production), a pixel budget in logical cells, *Auto tune* (reads size, detail and colour spread and sets sampling, palette count and dither), *Fit grid to budget*, and the style deck: 30 production recipes with a category filter, search, favourites, *Smart Match* (scores each recipe against the current image), *Compare 4* and *3 Variants*.

## 03 Resolution and framing
Grid width and height (linked by aspect lock), source pixels per cell, resolution multiplier, grid density slider, and the fit mode: contain, cover, stretch.

## 04 Sampling and edges
Sampling: area average (default), edge-aware area sample, smooth canvas sample, nearest neighbour. An edge map is computed for cleanup and adaptive reconstruction; the *Edge map* preview tab shows it.

## 05 Colour system
Palette mode: auto extract, style preset, custom. Colour count, minimum separation, locked colours, background colour detection and transparency, contrast and saturation nudges.

## 06 Dither
Fifteen modes: Floyd-Steinberg, Atkinson, Stucki, Burkes, Sierra, Sierra Lite, Jarvis-Judice-Ninke, random threshold, blue-noise style, clustered dot, checker transition, sparse transition, Bayer 2x2, 4x4 and 8x8. Strength, serpentine diffusion, pattern scale.

## 07 Cleanup
Neighbour cleanup passes with an isolation threshold, island removal by fragment size, stair-step regularisation, edge protection strength.

## 08 SVG and PNG export
Master SVG, optimised SVG, pixel form (square, inset tile, diamond, beveled, dot), PNG 1x to 16x with transparent or flattened background, mask PNG, ZIP package, copy SVG.

## 09 Saved settings
Named presets in localStorage, JSON import and export, undo / redo of settings.

## 10 Sharp Pixel style grammar
Per-cell or per-region texture grammar: classic, cluster, weave, facet, dissolve, cross, engrave.

## 11 Bulk automation
Runs a preset over the whole queue or a folder and packages results as a ZIP with SVG, PNG and JSON per image.

## 12 Folder rules
Maps folder names to presets so a bulk run routes each folder automatically.

## 13 Sprite sheet
Tile size, columns, padding; exports a packed PNG atlas and a JSON frame table.

## 14 GIF / Video
Frame extraction (count, stride, trim), GIF and WebM export (frame rate, duration, scale, bitrate), per-frame FX phase, animated SVG export.

## 15 Adaptive reconstruction
Variable detail density driven by the edge map; regularisation strength. *Palette interpolation* scales the dither strength of module 06 (70% by default) and only applies while this module is on; with it off, dither runs at the strength set in module 06.

## 16 Perceptual tone shaping
Shadow, mid and highlight curves applied before quantisation.

## 17 AI semantic zones + mask
Segmentation engines: heuristic (always available), SegFormer B0 ADE20K (default AI model), SegFormer B3 ADE20K. Device: auto, WebGPU, CPU / WASM. Zones can carry their own dither, palette and FX settings; a painted mask overrides the zones.

## 18 Pattern lab
Custom 4x4 and 8x8 ordered-dither tiles, editable cell by cell.

## 19 Collection style system
Fingerprints up to 10 example images and scores presets against them so a set of conversions stays consistent; locks the master palette.

## 20 GPU 4K preview
WebGL render of the output at up to 4K with an *Export GPU preview PNG* button.

## 21 FX lab
Base renderers: none, mono halftone, CMYK halftone, ASCII standard / dense / minimal / blocks / technical / hatching, Braille dots, Matrix digits, VHS / digital / weird / chromatic glitch, crosshatch, line art, engraving, stipple, Kuwahara lite. Post: CRT curvature and scanlines, bloom, chromatic aberration, film grain, vignette. Stack, randomise, animate; export FX PNG, GIF, WebM, animated SVG.

## 22 Procedural texture overlay
A non-destructive procedural texture blended over the output.
