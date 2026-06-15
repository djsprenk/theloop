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

## CSS conventions

- New sections go at the bottom of `styles.css` with a `/* === Section name === */` comment block header matching the existing style
- The `.btn`, `.section-eyebrow`, `.section-title`, `.section-body`, `.container`, `.faq-*`, `.team-*` classes are shared utilities — reuse them before adding new ones
- `color-mix(in srgb, var(--clay) 20%, transparent)` is the established pattern for transparent tints of brand colors
