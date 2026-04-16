---
title: navigation.yml
layout: default
nav_order: 2
parent: Data Folder
---

# `_data/navigation.yml`

Defines the main navigation menu items rendered by `_header-and-nav.html`.

## Role

Single source of truth for top-bar navigation links. Consumed by `_header-and-nav.html` via `site.data.navigation`. Also manually looped in `pages/index.md` (which does not use the standard includes).

## Data Structure

Array of objects. Each item:

```yaml
- title: "Link Label"
  url: /path-or-full-url
  excerpt: ""        # not currently used in nav rendering
  image: ""          # not currently used in nav rendering
```

| Field | Type | Purpose |
|---|---|---|
| `title` | string | Displayed link text in the nav bar |
| `url` | string | Link href; can be a root-relative path or a full `https://` URL |
| `excerpt` | string | Unused by current nav template; reserved for future use |
| `image` | string | Unused by current nav template; reserved for future use |

## External Link Detection

In `_header-and-nav.html`, any `url` containing `"http"` is treated as external:

- Rendered without `site.baseurl` prefix
- Opens in a new tab (`target="_blank"`)

Internal links (root-relative paths) get `site.baseurl` prepended automatically.

## Active State

`_header-and-nav.html` marks the current page active with:

```liquid
if page.url == nav.url
	active
endif
```

This is an exact string comparison. The `url` value in this file must exactly match the `permalink` defined in the target page's front matter.

## Used By

- `_includes/_header-and-nav.html` — standard nav rendering
- `pages/index.md` — manual loop (inline duplication of nav logic)

## Customization Notes

- **Adding a link:** Append a new list item with `title` and `url`. External URLs (starting with `http`) automatically open in a new tab.
- **Removing a link:** Delete the list item. No other files need updating (except `pages/index.md`, which manually duplicates this loop).
- **Active state precision:** Internal `url` values must exactly match the page's `permalink`. For example, a page with `permalink: /collection` needs `url: /collection` (not `/collection/`).
- **`excerpt` and `image` fields:** These are currently unused in the nav template but are present in the data structure. They could be used to add dropdown descriptions or icons if the nav template is extended.
- **`pages/index.md` sync:** Because `pages/index.md` uses `layout: blank` and manually loops `site.data.navigation`, nav changes here automatically apply to that page too — but any nav markup changes to `_header-and-nav.html` must be manually mirrored in `pages/index.md`.
