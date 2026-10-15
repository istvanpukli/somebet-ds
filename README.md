# Somebet design system

A themeable design system for the registration and login flow of a regulated betting product, built in Figma with native variables and exported to plain CSS custom properties. Somebet is a fictional brand.

**[Live demo](https://istvanpukli.github.io/somebet-ds/)** · **[Case study](https://claude.ai/artifact/WogGfVUHxqcTFa2WTYctiM)**

## What's here

| Path | Contents |
| --- | --- |
| `tokens/brand-somebet.css` | 45 brand roles (colours, fonts, radii) on `[data-brand="somebet"]` |
| `tokens/theme.css` | 81 theme tokens for Dark (default) and Light |
| `tokens/context.css` | 40 `--ctx-*` tokens in five surface contexts: Default, Alternate, Accent, Alternate accent, Header |
| `tokens/layout.css` | Space, size and type tokens; Compact by default, Expanded through a container query at 1024px |
| `demo/index.html` | A login screen, buttons, a select and a promo card, built only from those tokens |

Every CSS variable name matches the variable's code syntax in Figma. See [`tokens/README.md`](tokens/README.md) for load order and usage.

## How it works

The values chain by alias: Brand → Theme → Context, with Layout alongside. Components read only `--ctx-*` names, so one class on a container re-skins everything inside it:

```html
<html data-brand="somebet" data-theme="light">
  <aside class="promo ctx-accent">…</aside>
</html>
```

In the demo, use the toolbar to switch the theme, the container width (Compact / Expanded) and the card's context.

A new brand ships one file with the same 45 brand roles; theme, context and layout files stay unchanged.

## Notes

- Field borders are a `<fieldset>` with an invisible `<legend>`, so the floating label sits in a gap in the border and works on any surface.
- Icons and logos are exported from the Figma library as SVG; they are not redrawn.
- No build step: open `demo/index.html` in a browser, or serve the folder.

Designed by István Pukli. Built with Claude Code from reviewed, phase-by-phase briefs.
