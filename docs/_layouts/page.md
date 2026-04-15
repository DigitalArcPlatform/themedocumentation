# `_layouts/page.html`

Standard content page layout — dark header band with title, then a full-width content area below.

## Role

The primary mid-level layout. Sits between `default` and the more specialized content layouts (`post`, `collection`, `item`, etc.). Renders a dark-background header section containing the page title and optional subheadline, followed by the page's Markdown or HTML body content.

## Front Matter

```yaml
layout: default
format: page
```

Extends `default`. Sets `format: page` for potential CSS targeting.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.subheadline` | page front matter | Optional smaller text above the main title in the header band |
| `page.title` | page front matter | Main heading displayed in the dark header band |

## Includes / Inherits

- Inherits: `default.html` (provides `<head>`, nav, footer, JS)
- `{{ content }}` — rendered body of the child layout or page

## Layout Chain Position

```
default → page → [collection, group, item, post, homepage, stories]
```

All specialized layouts inherit from `page`, which means changes to `page.html` affect every layout in that chain.

## Used By

- `_layouts/post.html`
- `_layouts/homepage.html`
- `_layouts/collection.html`
- `_layouts/group.html`
- `_layouts/item.html`
- `_layouts/stories.html`
- Any page with `layout: page` in front matter

## Customization Notes

- **Header band:** The dark header is a styled `<div>` — adjust its background color or padding in `main.css` (target the class on that div) rather than editing this file.
- **`subheadline`:** Optional. If omitted from a page's front matter, the element renders as empty but doesn't break layout.
- **Full-width vs. contained:** The content area uses a Foundation `grid-container`. To make individual pages go full-width, override the container on those pages' layouts rather than changing it here (which would affect all pages).
