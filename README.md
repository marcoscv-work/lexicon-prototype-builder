# Lexicon Prototyping Kit

Vanilla HTML/CSS implementation of the [Lexicon Design System](https://liferay.design/lexicon/) (Liferay's Clay UI). Zero dependencies — open any file in a browser and it works.

Built for rapid AI-assisted prototyping: paste the CSS files into context, describe a screen, get working HTML.

---

## Files

| File | Purpose |
|------|---------|
| `tokens.css` | Design tokens — colors, spacing, typography, shadows, z-index (light mode) |
| `tokens-high-contrast.css` | Light high-contrast overrides; use `.hc` class or `prefers-contrast: more` |
| `tokens-dark.css` | Dark mode + dark high-contrast overrides; use `.dark` / `.dark-hc` classes or `prefers-color-scheme: dark` |
| `components.css` | All component styles (imports after tokens) |
| `components.html` | Living component library — every variant in one page |
| `document-manager.html` | Example prototype: Documents & Media app |
| `icons.svg` | Full Clay icon sprite (513 symbols, source file) |
| `icons-sprite.html` | Extracted inline sprite (legacy, use the inline block in components.html) |

[⬇ Download ZIP](https://github.com/marcoscv-work/lexicon-prototype-builder/archive/refs/heads/main.zip)

---

## Usage

### In a new prototype

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="stylesheet" href="tokens.css">
  <link rel="stylesheet" href="tokens-high-contrast.css"> <!-- optional -->
  <link rel="stylesheet" href="components.css">
</head>
<body>
  <!-- paste inline SVG sprite here (copy from components.html <body> opening) -->

  <!-- your prototype markup -->
</body>
</html>
```

### Theme activation

```html
<!-- Light high contrast -->
<html class="hc"> … </html>
<html data-theme="high-contrast"> … </html>   <!-- auto: prefers-contrast: more -->

<!-- Dark -->
<html class="dark"> … </html>
<html data-theme="dark"> … </html>             <!-- auto: prefers-color-scheme: dark -->

<!-- Dark high contrast -->
<html class="dark-hc"> … </html>
<html data-theme="dark-hc"> … </html>
```

The component library (`components.html`) includes a floating theme switcher (top-right) that toggles all four themes and persists the selection via `localStorage`.

> **Icons**: browsers block external SVG `<use>` on `file://`. Copy the inline `<svg style="display:none">…</svg>` block from `components.html` immediately after `<body>`.

### Reference the component library

Open `components.html` in a browser. Every component section shows the exact markup to copy.

---

## Component inventory

### Foundations
- **Colors** — full palette with semantic variants (`-d2` → `-l3` scales)
- **Spacing** — `--spacing-1` (2px) through `--spacing-15` (120px)
- **Typography** — `h1`–`h6`, text utilities, truncation
- **Border radius** — `sm` / `md` / `lg` / `full`

### Components
- **Buttons** — primary / secondary / borderless / danger / success / warning / info / link; sizes xs–lg; pill; icon-only (monospaced); button groups
- **Forms** — text / select / textarea; states (error, success, disabled); checkbox; radio; toggle switch
- **Input Group** — prefix/suffix text, button append, inset icons
- **Alerts** — success / info / warning / danger; dismissible; fluid; feedback; inline
- **Badges** — all variants including dark/light; badge-item with text truncation
- **Labels** — standard / large / inverse (filled) / dismissible
- **Cards** — basic; asset (`card-type-asset`) with aspect-ratio; template (selectable); interactive
- **Navigation** — dark navbar; application bar; sidebar menu; stacked nav
- **Navigation Bar** — horizontal secondary nav, light/secondary variants
- **Management Bar** — default filter bar; primary (selected state); subnav-tbar with active filters
- **Breadcrumb** — standard; in breadcrumb-bar; truncated items
- **Pagination** — with prev/next and first/last
- **Tables** — standard; sm; bordered; with sticker avatars and label status
- **Tabs** — underline (default); button tabs; justified
- **Dropdowns** — default; with icons; sections + subheaders + captions
- **Modals** — default; small/large; status variants (success/info/warning/danger)
- **Stickers** — initials; icon; positioned (top-left/right, bottom-left/right); overlay badge
- **Progress & Loading** — bar variants; progress groups; striped/animated; spinner sizes/colors; squares loader
- **Multi-step Nav** — wizard with complete/active/pending states
- **Sheets** — form containers with header/section/footer
- **Misc** — tooltips; empty state

### Icons
530+ Clay icons via inline SVG sprite. Usage:
```html
<svg class="lexicon-icon" aria-hidden="true"><use href="#pencil"></use></svg>
```
Size modifiers: `lexicon-icon-sm` · `lexicon-icon-lg` · `lexicon-icon-xl` · `lexicon-icon-2xl`

---

## Design tokens quick reference

```css
/* Colors */
var(--color-primary)       /* #0B5FFF */
var(--color-success)       /* #287D3C */
var(--color-warning)       /* #B95000 */
var(--color-danger)        /* #DA1414 */
var(--color-info)          /* #2E5AAC */
var(--color-dark)          /* #272833 */
var(--color-secondary)     /* #6B6C7E */

/* Spacing */
var(--spacing-3)   /*  8px */
var(--spacing-5)   /* 16px */
var(--spacing-7)   /* 24px */
var(--spacing-8)   /* 32px */

/* Typography */
var(--font-size-sm)    /* 12px */
var(--font-size-base)  /* 14px */
var(--font-size-md)    /* 16px */
var(--font-weight-semi)  /* 500 */
var(--font-weight-bold)  /* 700 */
```

---

## Prototyping with AI

The intended workflow:

1. Give the AI `tokens.css` + `components.css` as context (or describe the design system).
2. Ask for a screen: *"Build a user management page with a management bar, table with stickers and status labels, and a creation modal."*
3. The AI outputs self-contained HTML using the existing classes.
4. Open the file in a browser — no build step, no npm.

The `document-manager.html` file is a reference example of a full prototype built this way.

---

## Source

Design system: [clayui.com](https://www.clayui.com)  
Icons: [clayui.com/images/icons/icons.svg](https://www.clayui.com/images/icons/icons.svg)
