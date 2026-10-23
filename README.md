# Lighthouse

A pixelated, one-bit lighthouse drawn live by a single WebGL2 fragment shader, with a one-page site to tweak it.

The island and town are a fixed 540 × 960 bitmap. The beam, its ordered dither, the ocean outlines, the rock ripples and the gulls are computed in the shader every frame.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole landing page: live preview, controls, code export. One file. |
| `lighthouse.js` | The shader and engine as a drop-in script (no dependencies). |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |
| `LICENSE` | MIT. |

## Use the component

```html
<div style="width: 300px; height: 520px">
  <canvas id="c" width="540" height="960"></canvas>
</div>
<script src="lighthouse.js"></script>
<script>
  const lh = Lighthouse.mount(document.getElementById('c'), {
    settings: { pattern: 'stripes', speed: 4 },
    fit: 'parent', // 'parent' (default), 'window' or false
  });
</script>
```

Live control: `lh.S.intensity = 0.6; lh.dirty = true;`, `lh.playing = false`, `lh.angle = 120`, `lh.stop()`, `lh.destroy()`.

Settings: `speed`, `angle`, `width`, `intensity`, `pattern` (`dots`, `stripes`, `noise`, `diamond`), `beamOn`, `wavesOn`, `ripples`, `birds`, `waveSpeed`, `waveScale`, `waveDots`, `dark`, `light`, `beamTint`, `beamColor`.

Under CommonJS it exports the same object: `const Lighthouse = require('./lighthouse.js')`. It needs WebGL2 and throws if the browser has none.

## Deploy on GitHub Pages

```bash
git init
git add .
git commit -m "Lighthouse"
git branch -M main
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

Then on GitHub: Settings, Pages, Source = "Deploy from a branch", Branch = `main`, folder = `/ (root)`, Save. After a minute the site is live at `https://<you>.github.io/<repo>/`.

Custom domain: add a file named `CNAME` containing the domain, point a CNAME DNS record at `<you>.github.io`, then tick "Enforce HTTPS" in the Pages settings.

## Run locally

Open `index.html` in a browser. To use `lighthouse.js` from a page, a plain `<script src>` works from `file://` too.

## Notes

- Fonts (Source Serif 4, IBM Plex Mono, Cormorant Garamond) load from Google Fonts, with system fallbacks.
- The page follows an ink-on-paper design: five palette tokens, hairline rules, light by default, dark opt-in from the footer.
