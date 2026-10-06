# radondemand — Abdominal radiology teaching library

Static site of interactive abdominal radiology lessons (body MRI, Doppler ultrasound) for radiology residents
(UH Cleveland / CWRU). Target: https://radondemand.vercel.app

No build step, no dependencies. Every page is a single self-contained HTML file
(only external request: Google Fonts, with system-font fallbacks).

## Layout
- `index.html` — landing page. Lesson catalog is the `GROUPS` array in its script.
- `lessons/<slug>/index.html` — one self-contained lesson each.
- `vercel.json` — clean URLs, trailing slash.

## Lessons
| Slug | Title | Original claude.ai artifact |
|---|---|---|
| snr-equation | The SNR equation: knobs, costs and tradeoffs in body MRI | https://claude.ai/artifact/TJSoQBAz32Cj5R7v9sZeaP |
| subtraction-maps | Subtraction maps on body MRI | https://claude.ai/artifact/N9Vouah52TJh7K4jPnLuW5 |
| dixon-fat-iron | In/opposed phase, multi-echo Dixon and fat–iron quantification | https://claude.ai/artifact/3TWbnECbK13PoTvuFk77c2 |
| dwi-adc | DWI, ADC and calculated b-values | https://claude.ai/artifact/M8EaTBg2UEyHKDpasaGZQv |
| mr-fingerprinting | MR Fingerprinting | https://claude.ai/artifact/DX2qjbJr9tVyB55663ebZD |
| liver-mrf | Liver MR Fingerprinting (companion to mr-fingerprinting) | https://claude.ai/artifact/FgGZevgD9W3se7WPvGxfC1 |
| doppler-console | Doppler ultrasound console trainer | https://claude.ai/artifact/23ZrmYKrejfPzaBssxpawy |

The repo copies are snapshots taken Oct 1, 2026. The claude.ai artifacts remain
the originals if you want to regenerate a lesson in chat.

## Run locally
    python3 -m http.server 8000

## Deploy
Import the repo in Vercel (Framework Preset: Other). Project name: `radondemand`.

## Adding a lesson
1. Create `lessons/<new-slug>/index.html` (self-contained).
2. Add an entry to `GROUPS` in `index.html` (title, url `lessons/<new-slug>/`, desc, covers, glyph).
