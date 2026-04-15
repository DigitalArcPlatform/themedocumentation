---
title: collection.html
layout: default
nav_order: 2
parent: '"_Layouts" Folder'

# `_layouts/collection.html`

Collection page layout — inherits the `page` header, then conditionally renders either the blog post list or the item grid based on the page URL.

## Role

Single layout that serves two distinct collection types: blog posts and exhibit items. The switch between them is driven by a URL pattern check. This means one layout file handles both `/blog` and `/collection` (or any non-blog collection URL).

## Front Matter

```yaml
layout: page
format: collection
```

Extends `page` (which extends `default`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.url` | Jekyll built-in | Checked for `"blog"` to determine which include to render |
| `page.title` | page front matter | Passed through to `page.html` header band |

## Conditional Logic

```liquid
{% if page.url contains "blog" %}
  {% include _postlist.html %}
{% else %}
  {% include _itemlist.html %}
{% endif %}
```

- URL contains `"blog"` → renders `_postlist.html` (blog entries from `_posts/`)
- Any other URL → renders `_itemlist.html` (exhibit items from `_items/`)

## Includes / Inherits

- Inherits: `page.html` → `default.html`
- Conditionally includes: `_postlist.html` or `_itemlist.html`

## Used By

Any page with `layout: collection` in front matter:

- `pages/collection.md` (renders item grid)
- Any blog index page with a URL path containing `"blog"` (renders post list)

## Customization Notes

- **URL-based switch:** The `contains "blog"` check is a substring match on the full page URL. A page at `/blog-archive` would also trigger the post list. If you need stricter matching, change the condition to `page.url == "/blog/"` or use a front matter flag instead.
- **Adding a third collection type:** To support a third collection (e.g. oral histories at `/oralhistories`), add an `elsif` branch with a new include or inline logic.
- **Page body content:** The page's Markdown body (`{{ content }}`) is not rendered by this layout — the include takes the entire content slot. To add a description above the grid, edit the relevant include (`_itemlist.html` or `_postlist.html`) rather than the page's Markdown body.
