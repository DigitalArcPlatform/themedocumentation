---
title: blank.html
layout: default
nav_order: 1
parent: "_Layouts Folder"
---

# `_layouts/blank.html`

Bare pass-through layout that outputs only `{{ content }}` with no wrapping HTML.

## Role

Used when a page needs to supply its own complete HTML document — its own `<head>`, nav, footer, and scripts — rather than inheriting the standard structure from `default.html`. Renders literally nothing except the page's own content.

## Front Matter

None.

## Variables Used

None.

## Includes / Inherits

None. Does not extend `default`.

## Used By

- `pages/index.md` — the theme's landing/about page, which has a custom design that does not share the standard nav or footer

## Customization Notes

- **When to use:** Choose `layout: blank` only when a page's design is entirely custom and incompatible with the standard header/footer. For pages that simply need a different content area, extend `page` instead.
- **Self-contained responsibility:** A `blank`-layout page must include its own `<head>` (charset, viewport, CSS), navigation, footer, and JS. Forgetting any of these is a common source of broken pages.
- **`pages/index.md` pattern:** That page manually loops `site.data.navigation` and duplicates the footer markup. If you add new nav items or update the footer, you must update both `_header-and-nav.html` / `_footer.html` and `pages/index.md` separately.
