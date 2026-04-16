---
title: itembox.html
layout: default
nav_order: 4
parent: Includes Folder
---

# `_includes/_itembox.html`

Renders a single item as a card thumbnail — image, title, contributor, short description, and filter data attributes.

## Role

Called inside loops in `_itemlist.html`, `group.html`, and `stories.html`. Receives an `item` variable from the calling loop and outputs one card `<div>` per invocation. The card's `data-categories` and `data-formats` attributes are read by the JavaScript filter system.

## Variables Used

All variables are properties of the `item` object passed from the calling loop context.

| Variable | Source | Purpose |
|---|---|---|
| `item.url` | Jekyll built-in | Used to extract filename and build item ID; also used as card link href |
| `item.categories` | item front matter | Array; joined to `data-categories` attribute for JS filtering |
| `item.format` | item front matter | String or array; joined to `data-formats` attribute for JS filtering |
| `item.itemphoto` | item front matter | Explicit image filename override |
| `item.photo` | item front matter | Alternate explicit image filename |
| `item.title` | item front matter | Card heading and link text |
| `item.contributor` | item front matter | Displayed below title |
| `item.shortdesc` | item front matter | Truncated to 30 words with "read more" link |
| `item.group` | item front matter | Used in group-based filtering contexts |
| `site.baseurl` | `_config.yml` | Prefixes all internal links |
| `site.urlimg` | `_config.yml` | Base path for item images |
| `site.placeholderimg` | `_config.yml` | Fallback image filename when no item image is found |
| `site.static_files` | Jekyll built-in | Looped to find an image whose path matches the item ID pattern |

## Image Resolution Logic

Images are resolved in this order:

1. `item.itemphoto` — explicit override in front matter
2. `item.photo` — alternate explicit field
3. Static file search — loops `site.static_files` looking for a file whose path contains the item ID (extracted from the filename portion of `item.url`)
4. `site.placeholderimg` — fallback if none of the above resolve

## Item ID Extraction

Liquid: `capture FileName` and then print `[ item.url | split: '/' | last ]`

The filename (e.g. `2019-10-01-0003`) becomes the `ItemID` used when searching `site.static_files` for a matching image.

## Used By

- `_includes/_itemlist.html`
- `_layouts/group.html`
- `_layouts/stories.html`

## Customization Notes

- **Card layout:** The card uses Foundation grid classes. Adjust column widths or card markup directly in this file.
- **Description truncation:** `truncatewords:30` is hardcoded. Change the integer to adjust excerpt length.
- **Image fallback:** Set `site.placeholderimg` in `_config.yml` to your preferred placeholder image filename.
- **Filter attributes:** `data-categories` and `data-formats` are consumed by `app.js`. If you rename these attributes, update the JS filter logic to match.
- **Calling convention:** Always pass the item via a `for item in ...` loop. This include does not accept named parameters.
