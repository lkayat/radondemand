# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands
No build, lint, or test tooling exists. Preview with `python3 -m http.server 8000` (or `python -m http.server 8000` on Windows) and open http://localhost:8000. Deploys via Vercel (Framework Preset: Other); `vercel.json` sets clean URLs and trailing slashes, so lesson links end in `/`.

## Structure
- `index.html`: landing page (title "RadOnDemand: Abdominal radiology"); a filterable card grid driven by the flat `LESSONS` array in its script. Each entry has `areas` (one or more of physics, ultrasound, fluoro, clinical, anatomy), `organs`, `sub` (subspecialty, "abdominal" for now), `badge`, `added` (YYYY-MM-DD, first publish date), `desc`, `covers`, `glyph`.
- `lessons/<slug>/index.html`: one self-contained lesson each (inline CSS/JS, no shared assets).
- Adding a lesson: create the file, then add a `LESSONS` entry (title, fullTitle, url `lessons/<slug>/`, areas, sub, organs, badge, added, desc, covers, glyph) and a thumbnail in `G`. Also add a row to the README lessons table.

## Context

Owner: Leo, radiologist and Vice-Chair of Innovation (UH Cleveland), Professor at CWRU.
Audience: radiology residents learning body MRI. Tone: plain, clinically precise, no marketing language.

## Conventions
- Keep it static: plain HTML/CSS/JS, no framework, no build step, no npm dependencies.
- Each lesson is ONE self-contained HTML file (the three liver lessons also load their `cases/` images). Inline CSS and JS. Google Fonts allowed, always with fallbacks.
- All images are synthetic phantoms generated in-browser (canvas). Never add real patient images, with one exception approved by Leo: the three liver lessons (`focal-liver-lesions`, `hepatobiliary-agents`, `hcc-lirads`) include de-identified case images from his own teaching files (all previously shown at international conferences), stored as JPEGs in a `cases/` folder next to each lesson. Keep those filenames generic (no names, dates or ID numbers), and do not add any other real patient images without his explicit say-so.
- Landing page: fonts Newsreader + Public Sans; light/dark via CSS variables; lesson list is data-driven from `LESSONS`.
- Lessons were originally built as claude.ai artifacts (no browser storage APIs, no network calls). Keep it that way.
- Check mobile (390px) and dark mode after edits.

## Style of lessons
Instrument Sans + Literata, interactive controls that change the image so the physics is visible.
When adding a lesson, match the existing lessons' look and add it to `LESSONS` in `index.html`.

There is no shared stylesheet; each lesson copies the same design system inline. Start a new lesson by copying the `<head>`/`<style>` block of the closest existing lesson (`dwi-adc` is the cleanest template), not by writing CSS from scratch. The shared pattern:

- **Tokens** (in `:root`, with dark overrides duplicated under `@media (prefers-color-scheme: dark) :root:not([data-theme="light"])` and `:root[data-theme="dark"]`): `--bg #EDF0F1`, `--panel`, `--ink`, `--muted`, `--line`, accent `--amber #C98A0C` (focus rings, slider accent, active tab, callout bar), `--cyan`, plus `--rose/--warn/--ok/--bad/--violet` and `--chip-*` as needed. Any new color needs a light and a dark value. Use `--ui` (Instrument Sans) for controls and body, `--read` (Literata) for h1/h2, `.lede`, `.read`, `.note`.
- **Page skeleton**: `.wrap` (max-width ~1240px) → `h1` (clamp 28–42px) → `.lede` → optional equation line → `.scen` pill buttons (teaching cases, `aria-pressed`) → `.note` (amber left bar, text changes per case) → `.stage` grid (images left, `.panel` with `.tabs` and `.ctl` slider rows right; collapses to one column at 980px) → numbered `h2` sections with `.read` prose.
- **Images**: black `.lightbox`/`.dark` container, `<canvas>` with `.cap` captions in light-gray on black, optional `.cbar` color bars. Canvases are rendered in JS from phantom models; give them `aria-label`.
- **Controls**: `.ctl` grid (label / range input / `output` with tabular-nums); `.mini` buttons; visible `:focus-visible` outline; `[hidden]` for inactive tabpanels.
- **Behavior**: choosing a teaching case sets control state; touching any control calls a `custom()`-style handler that clears the case selection and swaps the note to "Custom settings". Redraw plots on resize and on `prefers-color-scheme` change.
- **Voice**: each lesson opens by telling the resident what they will do on the page, then explains the pitfall or QA step. Plain, clinically precise, no marketing language.

Every lesson starts with a `<nav class="back">` link to `../../` ("← All lessons") above the h1, uses `.wrap` max-width 1240px, and ends with a `<p class="foot">` disclaimer that closes with "For teaching only; not for clinical use." Keep all three in new lessons.

## Applying updated lessons
When Leo hands over a revised lesson file (exported from claude.ai), re-apply these local adjustments before committing, because the export lacks them:
- Back link `<nav class="back"><a href="../../">&larr; All lessons</a></nav>` and its `.back` styles. In `doppler-console` it is a 26px strip above `.app` (top-left of the frame), and `.app` height is `calc(100dvh - 26px)`.
- Vercel Web Analytics snippet before `</head>` (the `window.va` stub plus `<script defer src="/_vercel/insights/script.js"></script>`), as on every page.
- Footer disclaimer ends with "For teaching only; not for clinical use."
- Doppler submodules are added inside `lessons/doppler-console/` (one catalog entry); no placeholder entries on the landing page.
- Landing page filters are Type (physics, ultrasound, fluoroscopy, clinical, anatomy; a lesson can have several) and Organ; the "New" badge is automatic for lessons whose `added` date is within `NEW_DAYS` (10) days.
- When re-exporting the three liver lessons, refresh their `cases/` folder from the artifact's published files too (Artifact `read` with `paths`), and check the filenames stay generic.
- `postsurgical-upper-gi` loads three.js r128 from cdnjs (the only runtime script dependency on the site, besides Google Fonts); the 3D pane falls back to a message if it cannot load.
- Site fixes that the exports lack (re-apply when re-exporting): `postsurgical-upper-gi` has `fitBox`/`fitTexts`/`fitLegend` (reserve the height of the longest caption, operation blurb and legend so the steps panel and the viewer do not move between steps); `prostate-mri-anatomy` has the `.vlab-ax` rules that keep the axial slider the same width (the level label sits on its own row).
