---
title: header-and-nav.html
layout: default
nav_order: 3
parent: Includes Folder
---

# `_includes/_header-and-nav.html`

Renders the sticky top navigation bar — site title, mobile menu toggle, and data-driven nav links with active-state detection.

## Role

Included once in `default.html` immediately after `<body>`. Outputs the Foundation sticky header, the off-canvas mobile title bar, and the desktop top-bar nav. Navigation items are looped from `site.data.navigation`.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.title` | `_config.yml` | Displayed as the site name in the mobile title bar |
| `site.baseurl` | `_config.yml` | Prefixes the home link (`/`) for mobile nav |
| `site.data.navigation` | `_data/navigation.yml` | Array of nav items; each item provides `title` and `url` |
| `page.url` | Jekyll built-in | Compared against `nav.url` to set the `active` CSS class on the current page |

## Includes / Inherits

None.

## Logic Notes

- **External link detection:** If a nav item's `url` contains `"http"`, the link renders with `target="_blank"` and no `site.baseurl` prefix. Internal links get `site.baseurl` prepended.
- **Active state:** `{% if page.url == nav.url %} active{% endif %}` adds the Foundation `active` class. This is an exact string match — permalink-style URLs (e.g. `/collection`) must exactly match the `url` value in `navigation.yml`.

## Used By

- `_layouts/default.html` (only direct caller)
- Inherited by all layouts that extend `default`

## Customization Notes

- **Nav items:** Edit `_data/navigation.yml` to add, remove, or reorder links. No changes to this file needed.
- **External links:** Any `url` starting with `http` automatically opens in a new tab.
- **Active state logic:** If you change a page's `permalink`, update the matching `url` in `navigation.yml` or the active indicator will break.
- **Mobile title:** The mobile bar shows `site.title`. To display a logo image instead, replace the `<span>` containing ` [ site.title ] ` with an `<img>` tag.
- **Foundation version:** The sticky/off-canvas markup is Foundation 6-specific. Upgrading Foundation requires reviewing this file for breaking markup changes.
