---
title: default.html
layout: default
nav_order: 3
parent: "_Layouts Folder"
---

# `_layouts/default.html`

Root layout template. Wraps every page with the full HTML document structure — `<head>`, header/nav, content slot, footer, and JS bundles.

## Role

The base of the layout inheritance chain. All other layouts (except `blank`) ultimately extend `default`. Sets up the HTML document, computes copyright year variables, and assembles the three structural includes around `{{ content }}`.

## Front Matter

None. `default.html` is the root layout and has no parent.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.sitedate` | `_config.yml` | Launch year; used to compute `SiteYear` for copyright range |
| `site.baseurl` | `_config.yml` | Prefixes JS asset paths |

## Computed Variables

These are captured inside `default.html` and made available to child includes (`_footer.html`):

| Variable | Computed As | Purpose |
|---|---|---|
| `SiteYear` | `{% capture SiteYear %}{{ timestamp | date: "%Y" }}{% endcapture %}` | Launch year extracted from `site.sitedate` |
| `NowYear` | `{% capture NowYear %}{{ site.time | date: '%Y' }}{% endcapture %}` | Current build year |

## Includes

In order:

1. `_head.html` — inside `<head>`
2. `_header-and-nav.html` — top of `<body>`
3. `{{ content }}` — rendered output of the child layout or page
4. `_footer.html` — end of page content
5. JS scripts — jQuery, what-input, Foundation JS, `app.js` (all from `site.baseurl/assets/js/`)

## Layout Chain

`default` ← `page` ← `post`
`default` ← `page` ← `homepage`
`default` ← `page` ← `collection`
`default` ← `page` ← `group`
`default` ← `page` ← `item`
`default` ← `page` ← `stories`
`default` ← `blank` (parallel, not inherited)

## Used By

All layouts except `blank`.

## Customization Notes

- **JS bundle order:** jQuery → what-input → Foundation → `app.js`. Changing the order will break Foundation's JavaScript components.
- **Adding global scripts:** Add additional `<script>` tags after `app.js` in this file to include them on every page.
- **Copyright year:** Set `site.sitedate` in `_config.yml` to your site's launch year (e.g. `2019`). The footer will automatically display a range once the current year advances past the launch year.
- **Body classes:** The `<body>` tag has no dynamic classes by default. Add `class="{{ page.layout }}"` or similar here to enable layout-specific CSS targeting.
