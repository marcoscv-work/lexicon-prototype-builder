# Lexicon Prototyping — Design Guide

How to make decisions when building screens with this kit. Apply the framework below every time you place an element.

---

## Decision Framework

Apply these steps in order before writing any markup.

### Step 1 — Classify the element

Identify what kind of element you're placing and look it up in the [component mapping](#component-mapping) below.

### Step 2 — Library priority (strict waterfall)

```
1. LEXICON COMPONENTS   ← always check here first
2. LEXICON FOUNDATIONS  ← colors, spacing, type tokens; never hardcode values
3. COMPOSITIONS         ← combine components + foundations for complex patterns
4. LEXICON ICONS        ← all icons; no exceptions, no external icons
```

- **Components first.** Every UI element maps to something in `components.css`. Check before building anything.
- **Foundations always.** Even when a component doesn't exist, all values come from `tokens.css`. No hex codes, no `px` literals outside of token definitions.
- **Compositions when needed.** Complex DXP patterns (list views, detail pages, wizards) are assembled from components + foundations. If the pattern isn't in the kit, compose it — don't fabricate new primitives.
- **Icons from the sprite only.** `<svg class="lexicon-icon"><use href="#icon-name"></use></svg>`. Zero exceptions.

### Step 3 — Fit rules

| Situation | Action |
|-----------|--------|
| Perfect match in components | Use it as-is |
| Close match, minor gap | Use the closest component; adapt with tokens, not extra CSS |
| No match | Compose from existing components + layout utilities |
| Still no match | Build from tokens only; document the deviation with a comment |

Never use external components, icons, or hardcoded values.

---

## Component Mapping

### Actions

| Intent | Component | Class |
|--------|-----------|-------|
| Primary action | Button primary | `.btn .btn-primary` |
| Secondary action | Button secondary | `.btn .btn-secondary` |
| Destructive action | Button danger | `.btn .btn-danger` |
| Low-emphasis action | Button borderless | `.btn .btn-borderless` |
| Link-style action | Button link | `.btn .btn-link` |
| Icon-only action | Button monospaced | `.btn .btn-monospaced` |
| Inline confirm/cancel | Button group | `.btn-group` |
| Action with icon | Inline item | `.inline-item .inline-item-before/after` inside `.btn` |

Button sizes: add `.btn-xs` `.btn-sm` `.btn-lg` — default is md.  
Pill shape: add `.btn-pill`.

### Status & Feedback

| Intent | Component | Class |
|--------|-----------|-------|
| Page-level message | Alert | `.alert .alert-{success\|info\|warning\|danger}` |
| Dismissible message | Alert | add `.alert-dismissible` |
| Full-width banner | Alert fluid | `.alert-fluid` |
| Inline field error/success | Alert feedback | `.alert-feedback .alert-{danger\|success}` |
| Count / quantity | Badge | `.badge .badge-{variant}` |
| Status indicator | Label | `.label .label-{variant}` |
| Removable tag | Label dismissible | `.label .label-dismissible` |
| Filled/inverse status | Label inverse | `.label .label-inverse-{variant}` |
| Loading state | Spinner | `<span class="loading-animation loading-animation-{sm\|md\|lg}">` |
| Progress | Progress bar | `.progress > .progress-bar .{success\|warning\|danger}` |

### Data Display

| Intent | Component | Class |
|--------|-----------|-------|
| Tabular data | Table | `.table` |
| Dense table | Table sm | `.table .table-sm` |
| Table with dividers | Table bordered | `.table .table-bordered` |
| Cards grid | Card | `.card` |
| Media/asset grid | Asset card | `.card .card-type-asset` |
| Selectable card | Template card | `.card .card-interactive .card-type-template` |
| Avatar / initials | Sticker | `.sticker .sticker-{color}` |
| Avatar in table | Sticker sm | `.sticker .sticker-sm` |

### Forms & Input

| Intent | Component | Class |
|--------|-----------|-------|
| Text input | Form control | `.form-control` |
| Select | Form control | `.form-control` on `<select>` |
| Textarea | Form control | `.form-control` on `<textarea>` |
| Input with button | Input group | `.input-group` |
| Input with icon | Input group inset | `.input-group-inset` |
| Checkbox (native) | Form check | `.form-check > .form-check-input` |
| Radio (native) | Form check | `.form-check > .form-check-input[type=radio]` |
| Checkbox (Clay style) | Custom control | `.custom-control .custom-checkbox` |
| Radio (Clay style) | Custom control | `.custom-control .custom-radio` |
| On/off toggle | Toggle switch | `.toggle-switch` |
| Form container | Sheet | `.sheet > .sheet-header .sheet-section .sheet-footer` |
| Error state | Form feedback | `.form-feedback-item .form-feedback-indicator` |

### Navigation & Chrome

| Intent | Component | Class |
|--------|-----------|-------|
| App top bar | Application bar | `.application-bar .navbar` |
| Dark site header | Navbar dark | `.navbar .navbar-dark` |
| Secondary horizontal nav | Navigation bar | `.navigation-bar > .navbar > .navbar-collapse > .navbar-nav` |
| Left sidebar (simple) | Nav menu | `.nav .nav-menu` |
| Vertical tree nav (multi-level) | Vertical nav | `.vertical-nav > nav.menubar.menubar-vertical.menubar-decorated > ul.nav-nested-margins` |
| Vertical stacked nav | Nav stacked | `.nav .nav-stacked` |
| Breadcrumb trail | Breadcrumb | `.breadcrumb > .breadcrumb-item` |
| List/asset pages | Management bar | `.management-bar .management-bar-default` |
| Selected state bar | Management bar primary | `.management-bar .management-bar-primary` |
| Active filters row | Subnav tbar | `.subnav-tbar` |

### Content Switching

| Intent | Component | Class |
|--------|-----------|-------|
| Section switcher | Tabs underline | `.nav-tabs > .nav-item > .nav-link` |
| Filter pills | Button tabs | `.nav-tabs-button > .nav-item > .nav-link` |
| Equal-width tabs | Tabs justified | add `.nav-justified` to `.nav-tabs` |
| Multi-step form | Multi-step nav | `.multi-step-nav > .multi-step-item` |

### Overlays

| Intent | Component | Class |
|--------|-----------|-------|
| Confirmation dialog | Modal | `.modal > .modal-dialog > .modal-content` |
| Destructive confirm | Modal danger | add `.modal-danger` to `.modal-header` |
| Context menu | Dropdown | `.dropdown > .dropdown-toggle` + `.dropdown-menu` |
| Brief hint | Tooltip | `.tooltip` + `.tooltip-inner` |

### Pagination & Lists

| Intent | Component | Class |
|--------|-----------|-------|
| Paginated list footer | Pagination bar | `.pagination-bar > .pagination-results` + `.pagination` |
| Empty list | Empty state | `.text-center` + icon + heading + description + action |

---

## Layout Utilities

### Autofit (flexible row)

The primary horizontal layout primitive. Use instead of ad-hoc flexbox.

```html
<div class="autofit-row autofit-row-center">
  <div class="autofit-col autofit-col-expand"><!-- grows --></div>
  <div class="autofit-col"><!-- fixed width --></div>
</div>
```

`autofit-row-center` — vertical center alignment  
`autofit-col-expand` — takes all remaining space  
Nest `autofit-row` inside cells for multi-column layouts.

### Inline items (icon + label in one line)

```html
<button class="btn btn-primary">
  <span class="inline-item inline-item-before">
    <svg class="lexicon-icon" aria-hidden="true"><use href="#plus"></use></svg>
  </span>
  New Item
</button>
```

`inline-item-before` — icon before text  
`inline-item-after` — icon after text  
`inline-item` alone — icon only, no text neighbor

### Typography tokens

```html
<h1>–<h6>          <!-- semantic headings, styled by tokens -->
<p class="text-muted">     <!-- --color-secondary -->
<small>                    <!-- --font-size-sm -->
<span class="text-truncate-inline">
  <span class="text-truncate">Long label…</span>
</span>
```

Never set `font-size`, `color`, or `font-weight` with hardcoded values. Use the token variables or the utility classes above.

---

## Token Rules

All values must come from `tokens.css`. Quick reference:

```css
/* Colors */
var(--color-primary)          /* #0B5FFF — main brand */
var(--color-secondary)        /* #6B6C7E — muted text, secondary actions */
var(--color-dark)             /* #272833 — headings, primary text */
var(--color-light)            /* #F1F2F5 — page background, hover fills */
var(--color-success)          /* #287D3C */
var(--color-warning)          /* #B95000 */
var(--color-danger)           /* #DA1414 */
var(--color-info)             /* #2E5AAC */

/* Spacing — always step in multiples */
var(--spacing-3)   /*  8px */
var(--spacing-4)   /* 12px */
var(--spacing-5)   /* 16px */
var(--spacing-6)   /* 20px */
var(--spacing-7)   /* 24px */
var(--spacing-8)   /* 32px */

/* Typography */
var(--font-size-sm)      /* 12px */
var(--font-size-base)    /* 14px — body default */
var(--font-size-md)      /* 16px */
var(--font-weight-semi)  /* 500 */
var(--font-weight-bold)  /* 700 */

/* Radius */
var(--rounded-sm)   /* 2px */
var(--rounded-md)   /* 4px */
var(--rounded-lg)   /* 8px */
var(--rounded-full) /* 9999px */

/* Shadows */
var(--shadow-sm)    /* card resting */
var(--shadow-md)    /* dropdown, popover */
var(--shadow-lg)    /* modal */
```

---

## Icons

All icons come from the inline SVG sprite. Copy the `<svg style="display:none">…</svg>` block from `components.html` into every prototype's `<body>`.

```html
<!-- Standard -->
<svg class="lexicon-icon" aria-hidden="true"><use href="#icon-name"></use></svg>

<!-- Sizes -->
<svg class="lexicon-icon lexicon-icon-sm">…</svg>   <!-- 12px -->
<svg class="lexicon-icon">…</svg>                    <!-- 16px default -->
<svg class="lexicon-icon lexicon-icon-lg">…</svg>   <!-- 24px -->
<svg class="lexicon-icon lexicon-icon-xl">…</svg>   <!-- 32px -->
<svg class="lexicon-icon lexicon-icon-2xl">…</svg>  <!-- 48px -->
```

Common names: `plus` `pencil` `trash` `search` `times` `check` `angle-left` `angle-right` `ellipsis-v` `caret-bottom` `info-circle-open` `warning-full` `check-circle-full` `ban` `user` `folder` `document-text` `home` `cog` `bell` `filter`

Browse all 530+ in the Icons section of `components.html`.

---

## Common Screen Patterns

### List / Browse screen

```
application-bar           ← app name, user avatar, global actions
navigation-bar            ← secondary section nav (optional)
management-bar-default    ← search, filter, sort, view toggle
subnav-tbar               ← result count + active filter labels (shown when filters active)
[table | card grid]       ← main content
pagination-bar            ← results text + page controls
```

### Detail / Form screen

```
application-bar
breadcrumb-bar            ← path back to list
sheet                     ← .sheet-header + .sheet-section(s) + .sheet-footer
  [form controls]
  .btn-group (Save / Cancel) inside sheet-footer
```

### Wizard / Multi-step

```
application-bar
multi-step-nav            ← steps with complete/active/pending states
sheet                     ← current step content
  .sheet-footer with Back / Next buttons
```

### Modal confirm

```html
<div class="modal">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h4 class="modal-title">Confirm action</h4>
        <button class="close btn btn-unstyled" type="button">
          <svg class="lexicon-icon"><use href="#times"></use></svg>
        </button>
      </div>
      <div class="modal-body">…</div>
      <div class="modal-footer">
        <div class="modal-item-last">
          <div class="btn-group">
            <button class="btn btn-secondary">Cancel</button>
            <button class="btn btn-primary">Confirm</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

For destructive confirms: add `.modal-danger` to `.modal-header`, change primary button to `.btn-danger`.

---

## Themes

Add the class to `<html>` to activate:

| Theme | Class |
|-------|-------|
| Light (default) | `class="light"` |
| Light high contrast | `class="hc"` |
| Dark | `class="dark"` |
| Dark high contrast | `class="dark-hc"` |

Auto-activates from OS preference when no explicit class is set (dark: `prefers-color-scheme: dark`, HC: `prefers-contrast: more`).

The `components.html` library has a floating theme switcher (top-right) that persists via `localStorage`.

---

## What to Avoid

| Don't | Do instead |
|-------|------------|
| Hardcode `#0B5FFF` | `var(--color-primary)` |
| Hardcode `16px` | `var(--spacing-5)` or `var(--font-size-md)` |
| Use `position: absolute` for layout | `autofit-row` / flexbox with tokens |
| Import external icons | Inline SVG sprite `<use href="#name">` |
| Build a custom input from scratch | Adapt `.form-control` + `.input-group` |
| Use `<img>` for icons | `<svg class="lexicon-icon">` |
| Leave placeholder text | Replace with realistic content |

---

## Deviation Protocol

When a component doesn't exist or doesn't fit:

1. Find the closest component in `components.html`.
2. Adapt it using only token overrides (inline `style="…"` with `var()` values is acceptable for one-off prototypes).
3. Leave a comment: `<!-- deviation: using card as X because Y doesn't exist in kit -->`.
4. Don't introduce new CSS classes — adapt tokens inline.

---

*Reference: `components.html` — live component library with every variant.*  
*Reference: `document-manager.html` — full prototype example.*
