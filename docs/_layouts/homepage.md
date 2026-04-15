---
title: homepage.html
layout: default
nav_order: 5
parent: Layouts Folder
---

# `_layouts/homepage.html`

Homepage/about layout — dark hero header with subtitle and title, then a two-column content area with site logo.

## Role

Designed for the main landing page of a site using this theme. Renders a dark hero band with `site.subtitle` and `site.title`, then a two-column Foundation grid: the left column holds the page's Markdown content (`{{ content }}`); the right column displays the site logo image. An email address is optionally shown at the bottom of the content column.

## Front Matter

```yaml
layout: default
format: homepage
```

Extends `default` directly (not through `page`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.subtitle` | `_config.yml` | Smaller text above the main title in the hero band |
| `site.title` | `_config.yml` | Main heading in the hero band |
| `site.baseurl` | `_config.yml` | Prefixes the logo image `src` path |
| `site.urlimg` | `_config.yml` | Base directory for site images |
| `site.sitelogo` | `_config.yml` | Filename of the logo image displayed in the right column |
| `site.email` | `_config.yml` | Contact email shown below content; suppressed if blank |

## Layout Structure

```
[dark hero band: site.subtitle | site.title]
[medium-8 content column] [medium-4 logo column]
[optional email]
```

The two-column split uses Foundation's `medium-8` / `medium-4` grid. On small screens, Foundation stacks the columns.

## Includes / Inherits

- Inherits: `default.html`
- `{{ content }}` — the page's Markdown body, rendered in the left column

## Used By

Any page with `layout: homepage` in front matter. Typically one page per site.

## Customization Notes

- **Hero text:** `site.subtitle` appears above `site.title`. Both come from `_config.yml` — changing them affects every use of this layout and also the standard `page` header.
- **Column widths:** Adjust `medium-8` / `medium-4` to change the content/logo split. Values must sum to 12 for Foundation's 12-column grid.
- **Logo:** Controlled by `site.urlimg` + `site.sitelogo`. The logo renders only in the right column; it does not appear in the hero band.
- **Email display:** `site.email` is shown as a plain `<em>` element (not a `mailto:` link). Edit the markup here if you want it to be a clickable link.
- **Responsive order:** Foundation `order` classes control column stacking order on small screens. Review the `cell` classes in this file if you need to change which column appears first on mobile.
