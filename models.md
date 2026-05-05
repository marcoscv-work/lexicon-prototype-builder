# AI Model Guide for Lexicon Prototyping

Recommendations for which models to use when generating prototypes with this kit.

---

## Recommended models

| Task | Model | Why |
|------|-------|-----|
| Full screen from description | `claude-opus-4-7` | Best at inferring layout intent and combining multiple components correctly |
| Iterating / tweaking existing prototype | `claude-sonnet-4-6` | Fast, accurate edits with good class awareness |
| Quick single-component snippet | `claude-haiku-4-5` | Lowest latency for small, bounded requests |

All three models are available via the [Anthropic API](https://www.anthropic.com/) and in [Claude Code](https://claude.ai/code).

---

## Context to provide

The models work best when given the CSS files directly in context. Provide them in this order:

```
1. tokens.css        ← design tokens (colors, spacing, type)
2. components.css    ← component classes
3. [optional] a reference prototype (e.g. document-manager.html)
```

Alternatively, describe the design system briefly:

> "Use Lexicon/Clay UI conventions. CSS classes follow BEM-like patterns: `.btn .btn-primary`, `.alert .alert-success`, `.badge .badge-danger`. Tokens are CSS custom properties: `var(--color-primary)`, `var(--spacing-5)`. Icons use inline SVG sprite: `<svg class="lexicon-icon"><use href="#icon-name"></use></svg>`."

---

## Prompting patterns

### New screen
```
Build a [screen name] prototype using Lexicon CSS classes.

Include:
- [list the main UI areas, e.g. "application bar with app name and notifications icon"]
- [list components needed, e.g. "management bar with filter/sort, card grid, empty state"]

Output a complete self-contained HTML file that imports tokens.css and components.css.
Copy the inline SVG sprite from the opening <body> tag of components.html.
```

### Specific component
```
Show the markup for a [component] using Lexicon/Clay classes. 
Variant: [e.g. "dismissible label with inverse-warning style"].
Reference: components.html #labels section.
```

### Iteration
```
In document-manager.html, change [X] to [Y].
Keep all existing classes and the inline SVG sprite intact.
```

---

## Key class patterns to include in prompts

When asking for specific layouts, naming these patterns helps the model produce correct output:

**Autofit row** (flexible horizontal layout):
```html
<div class="autofit-row autofit-row-center">
  <div class="autofit-col autofit-col-expand">…content…</div>
  <div class="autofit-col">…actions…</div>
</div>
```

**Inline icon in button**:
```html
<button class="btn btn-primary">
  <span class="inline-item inline-item-before">
    <svg class="lexicon-icon" aria-hidden="true"><use href="#plus"></use></svg>
  </span>
  Add Item
</button>
```

**Management bar + subnav**:
```html
<div class="management-bar management-bar-default">…filter row…</div>
<div class="subnav-tbar">…result count + active filter labels…</div>
```

**Asset card structure**:
```html
<div class="card card-type-asset">
  <div class="aspect-ratio aspect-ratio-4-to-3">…thumbnail…</div>
  <div class="card-row">
    <div class="autofit-col autofit-col-expand">
      <h4 class="card-title"><span class="text-truncate-inline"><span class="text-truncate">…</span></span></h4>
      <div class="card-detail">…metadata…</div>
    </div>
    <div class="autofit-col">…actions…</div>
  </div>
</div>
```

---

## What the models tend to get wrong

- **Icon hrefs**: must be `href="#name"` (not `xlink:href`, not an external path) — the sprite is inline.
- **Sticker positions**: require `position:relative` on the parent and `sticker-absolute` on the sticker itself.
- **Input group inset**: the inset-item is `position:absolute`, so the wrapper needs `position:relative`.
- **Progress bar color**: the color modifier goes on `.progress-bar`, not on `.progress` (e.g. `<div class="progress-bar success">`).
- **Tab active state**: `tab-pane.active` shows the pane; without it the content is `display:none`.

---

## Model API usage

```js
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic();

const message = await client.messages.create({
  model: "claude-sonnet-4-6",   // or claude-opus-4-7 for complex screens
  max_tokens: 8192,
  messages: [
    {
      role: "user",
      content: [
        { type: "text", text: tokensCSS },      // contents of tokens.css
        { type: "text", text: componentsCSS },  // contents of components.css
        { type: "text", text: "Build a user management screen with…" }
      ]
    }
  ]
});

console.log(message.content[0].text);
```

Latest model IDs:
- `claude-opus-4-7`
- `claude-sonnet-4-6`
- `claude-haiku-4-5-20251001`
