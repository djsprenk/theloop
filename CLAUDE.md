# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Local development

```bash
npx serve .
```

Visit `http://localhost:3000`. No build step — changes are live on reload.

## Deployment

Push to `main`. GitHub Pages serves directly from the repo root. Takes a few minutes to propagate.

## Architecture

Pure static HTML/CSS/JS — no framework, no bundler, no package manager.

**Pages:**

- `index.html` — main community landing page
- `academy.html` — The Loop Academy course page (separate paid program)

Both pages share a single `styles.css`. Academy-specific styles are appended at the bottom of that file under their own comment sections. The `academy.html` page uses `class="page-academy"` on `<body>` for potential page-scoped overrides.

**Icons** are SVG symbols in `assets/icons/sprite.svg`, referenced inline via:

```html
<svg width="18" height="18" aria-hidden="true">
  <use href="assets/icons/sprite.svg#symbol-id"></use>
</svg>
```

To add a new icon, add a `<symbol id="name" viewBox="...">` to the sprite file.

**Design tokens** are CSS custom properties on `:root` in `styles.css`. Always use these — never hardcode colors or spacing values. Key tokens:

- Colors: `--midnight`, `--deep-plum`, `--parchment`, `--clay`, `--sand`, `--warm-white`
- Semantic roles: `--bg`, `--surface`, `--accent`, `--text-primary`, `--text-secondary`, `--text-muted`
- Type scale: `--text-sm` through `--text-hero` (all `clamp()`-based)
- Spacing: `--space-1` through `--space-32`

**Navigation** has three responsive states: full at >960px, collapsed links at 960px, hamburger menu at <600px. The toggle is wired via inline JS at the bottom of each page.

**Accordions** (FAQ, curriculum) use native `<details>/<summary>` — no JS required. The open/close chevron is a CSS `::after` pseudo-element that rotates on `[open]`.

**Countdown timer** on `academy.html` targets `2026-06-30T17:00:00Z` (June 30, 2026 at 19:00 CEST). When the date passes, the wrapper is replaced with an "enrollment is open" message. A `.countdown-date` line below the counter uses `Intl.DateTimeFormat` to show the target in the visitor's local timezone.

## CSS conventions

- New sections go at the bottom of `styles.css` with a `/* === Section name === */` comment block header matching the existing style
- The `.btn`, `.section-eyebrow`, `.section-title`, `.section-body`, `.container`, `.faq-*`, `.team-*` classes are shared utilities — reuse them before adding new ones
- `color-mix(in srgb, var(--clay) 20%, transparent)` is the established pattern for transparent tints of brand colors
