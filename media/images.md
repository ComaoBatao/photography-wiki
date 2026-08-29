# Images & Animated GIFs

## Create an image item

```mcfunction
/photography image "Old Photograph" item "photos/old_house.png" ocultar true
```

Or use HTTP(S):

```mcfunction
/photography image "Web Photograph" item "https://example.com/photo.png" ocultar true
```

## Supported formats

Local validation accepts:

- PNG
- JPG
- JPEG
- GIF

The decoder supports still images and animated GIFs.

## Viewer controls

| Input | Behavior |
|---|---|
| Mouse wheel | Zoom in/out |
| Left-drag | Pan when zoomed above 100% |
| ESC | Close viewer |

Zoom range:

```text
25% to 800%
```

Each wheel step multiplies/divides zoom by approximately 1.15.

The initial image is fit into the available viewport but is not upscaled beyond its native size by the base fit calculation.

## Image download/file limits

Photography rejects an image larger than **16 MB** after local size check or HTTP download.

Online image requests use finite connect/request timeouts, so a dead image host does not wait forever.

## GIF limits

The GIF decoder protects the client from extreme files:

- Maximum dimension: **4096 px** on either axis.
- Maximum GIF frames: **300**.
- Maximum total decoded frame pixels: **24,000,000**.
- GIF frame delay is clamped to at least **20 ms**.

If a GIF exceeds these safety limits, the viewer shows an error instead of trying to allocate unbounded memory.

## Subfolders

This file:

```text
mods/photography/image/evidence/night1/cam.png
```

is referenced as:

```text
evidence/night1/cam.png
```
