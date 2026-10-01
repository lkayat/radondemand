# Context for Claude Code

Owner: Leo, radiologist and Vice-Chair of Innovation (UH Cleveland), Professor at CWRU.
Audience: radiology residents learning body MRI. Tone: plain, clinically precise, no marketing language.

## Conventions
- Keep it static: plain HTML/CSS/JS, no framework, no build step, no npm dependencies.
- Each lesson is ONE self-contained HTML file. Inline CSS and JS. Google Fonts allowed, always with fallbacks.
- All images are synthetic phantoms generated in-browser (canvas). Never add real patient images.
- Landing page: fonts Newsreader + Public Sans; light/dark via CSS variables; lesson list is data-driven from `GROUPS`.
- Lessons were originally built as claude.ai artifacts (no browser storage APIs, no network calls). Keep it that way.
- Check mobile (390px) and dark mode after edits.

## Style of lessons
Instrument Sans + Literata, interactive controls that change the image so the physics is visible.
When adding a lesson, match the existing lessons' look and add it to `GROUPS` in `index.html`.
