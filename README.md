# RadOnDemand: Abdominal radiology

Interactive phantoms for learning body imaging by doing: static site of abdominal radiology lessons (body MRI, Doppler ultrasound, clinical tutorials) for radiology residents
(UH Cleveland / CWRU). Target: https://radondemand.vercel.app

No build step, no dependencies. Every page is a single self-contained HTML file
(only external request: Google Fonts, with system-font fallbacks).

## Layout
- `index.html` — landing page. Lesson catalog is the `LESSONS` array in its script (filterable by type and organ).
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
| mr-defecography | MR defecography for pelvic floor weakness | https://claude.ai/artifact/E7kUTeVnJvGz8vixKjKhNV |
| mri-fistula-in-ano | MRI of fistula-in-ano: anatomy, classification and reporting | https://claude.ai/artifact/J1ScdgcjmVJjAsu4FZvjd8 |
| prostate-mri-anatomy | Prostate anatomy on MRI: zones, measurements, BPH and treatment changes | https://claude.ai/artifact/14HDbdsaSSdSfHh4Mp1y9X |

The repo copies are snapshots taken Oct 1, 2026. The claude.ai artifacts remain
the originals if you want to regenerate a lesson in chat.

## Run locally
    python3 -m http.server 8000

## Deploy
Import the repo in Vercel (Framework Preset: Other). Project name: `radondemand`.

## Adding a lesson
1. Create `lessons/<new-slug>/index.html` (self-contained).
2. Add an entry to `LESSONS` in `index.html` (title, fullTitle, url `lessons/<new-slug>/`, area, sub, organs, badge, desc, covers, glyph) and a thumbnail in `G`.
