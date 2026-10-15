# Somebet tokens (CSS)

Generated from the Figma file "Somebet DS Components" (then named "DS Components") (collections Brand, Theme, Context, Layout) on 2026-10-14. Primitives are not exported; their values are resolved into `brand-somebet.css`, `layout.css`, and the few theme and context tokens that alias a Primitive directly. Every CSS variable name equals the variable's WEB code syntax in Figma.

## Load order

```html
<link rel="stylesheet" href="tokens/brand-somebet.css">
<link rel="stylesheet" href="tokens/theme.css">
<link rel="stylesheet" href="tokens/context.css">
<link rel="stylesheet" href="tokens/layout.css">
```

Order matters: Theme references Brand, Context references Theme and Brand, and a `.ctx-*` class must come after `[data-theme]` rules.

| File | Variables | Contents |
| --- | --- | --- |
| `brand-somebet.css` | 45 (`--brand-*`) | Raw brand values on `[data-brand="somebet"]` |
| `theme.css` | 81 (`--surface`, `--on-surface-high`, `--primary`, ...) | Dark (default) and Light, as `var(--brand-*)` |
| `context.css` | 40 (`--ctx-*`) | Five contexts. Default, Alternate and Header reference theme tokens; Accent and Alternate accent reference brand tokens directly |
| `layout.css` | 39 (`--space-*`, `--size-*`, `--type-*`, `--logo-form`) | Compact on `:root`, Expanded in a container query |

Theme and Context use different prefixes (`--on-surface-high` vs `--ctx-on-surface-high`), so there are no name collisions. Components should read `--ctx-*` only.

## Switch brand

Set `data-brand` on `<html>` and load that brand's file instead of `brand-somebet.css`. A new brand ships a `brand-<name>.css` that defines the same 45 variable names; theme, context and layout files are unchanged.

## Switch theme

Set `data-theme="dark"` or `data-theme="light"` on `<html>` (the same element as `data-brand`, because theme variables resolve against the brand variables on that element). Dark is the default with no attribute. A nested `[data-theme]` element recomputes the contexts inside it.

## Switch context

Add one class to any element; everything inside it follows:

- `.ctx-alternate`: the inverted surface (light card on a dark page, navy card on a light page).
- `.ctx-accent`: gold, the same in both themes. Navy primary, white secondary.
- `.ctx-alternate-accent`: vivid purple, the same in both themes, for a second strong offer next to the first.
- `.ctx-header`: the brand header surface.

With no class, the Default context applies. A floating snackbar always uses Default; an embedded banner takes its parent's context.

```css
.card { background: var(--ctx-surface-variant); color: var(--ctx-on-surface-high); }
```

`--ctx-logo-context` (`"Default"` or `"Accent"`) and `--logo-form` (`"Compact"` or `"Horizontal"`) tell the app which logo artwork to show. The logo itself is not token-coloured.

## Layout (Compact / Expanded)

Wrap a screen in a container:

```css
.layout { container-type: inline-size; }
```

Compact values sit on `:root`. When the nearest `.layout` ancestor is 1024px wide or more, Expanded values are applied to its direct children (a container query cannot style its own container) and inherited from there. Put your content in a child of `.layout`. This is a container query, not a viewport media query, so a narrow screen inside a wide container gets Expanded.

## Changes since the 2026-10-12 export

- Accent is now gold and Alternate accent vivid purple; both are theme-independent and reference Brand roles directly.
- New brand roles: `--brand-primary-200`, `-400`, `-650`, `-750`, `--brand-secondary-700`, and `--brand-alt-accent-surface`, `-surface-raised`, `-hover`, `-pressed`, `-subtle`.
- Highlight text on light surfaces is `--brand-primary-750` (4.55:1). Selection indicators (radio dot, focus ring on light surfaces) use the new `--ctx-on-surface-selected`, which is `--brand-primary-650` (3:1) on light surfaces.
- Disabled fills on Alternate and Header surfaces follow the surface, not the page theme (new `--alternate-*-disabled` and `--header-*-disabled`).
- New `--ctx-logo-context`.
- `--background` is now the darkest neutral (`--brand-neutral-950`) in Dark and white (`--brand-neutral-0`) in Light, so the page sits behind surfaces instead of matching them.
- Not exported: elevation (effect styles are not variables).
