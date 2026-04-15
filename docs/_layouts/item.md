---
title: item.html
layout: default
nav_order: 6
parent: "_Layouts" Folder
---

# `_layouts/item.html`

Individual item page layout — two-column card with media (image, video, or audio) plus metadata, followed by full item description and a Dublin Core metadata table.

## Role

Used by every file in `_items/`. Renders a rich item record: left column for media (YouTube embed, static image, or audio player), right column for contributor metadata, then the full Markdown body, and finally a Dublin Core table generated from `site.data.metadata.fields`.

## Front Matter

```yaml
layout: page
format: item
```

Extends `page` (which extends `default`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.url` | Jekyll built-in | Used to extract item ID from filename |
| `page.embedurl` | item front matter | YouTube or other embed URL; triggers video embed if present |
| `page.photo` | item front matter | Explicit image filename override |
| `page.shortdesc` | item front matter | Brief description shown in the right column header area |
| `page.contributor` | item front matter | Person who contributed the item |
| `page.contributorquote` | item front matter | Pull quote from the contributor |
| `page.creator` | item front matter | Original creator of the object |
| `page.externalurl` | item front matter | Link to the item at an external source |
| `page.teammember` | item front matter | Project team member who assisted |
| `site.data.metadata.fields` | `_data/metadata.yml` | Ordered map of field names → display labels for the Dublin Core table |
| `site.static_files` | Jekyll built-in | Looped multiple times to find matching image and audio files by item ID |
| `site.baseurl` | `_config.yml` | Prefixes all internal asset paths |
| `site.urlimg` | `_config.yml` | Base path for item images |

## Item ID Extraction

```liquid
{% capture FileName %}{{ page.url | split: '/' | last }}{% endcapture %}
```

The filename (e.g. `2019-10-01-0003`) becomes `ItemID`, used to search `site.static_files` for matching assets.

## Media Resolution Logic

Media is displayed in the left column in this priority order:

1. **YouTube embed** — if `page.embedurl` is set, parses the URL to extract the video ID (handles both `youtu.be/ID` and `youtube.com/watch?v=ID` formats) and renders an `<iframe>`
2. **Static image** — loops `site.static_files` for a file whose path contains `ItemID`; renders as `<img>`
3. **Audio player** — if a `.mp3` file matching `ItemID` is found in `site.static_files`, renders an HTML5 `<audio>` player with a transcript download link (looks for a file containing `ItemID + "_Transcript"`)
4. **Explicit photo** — `page.photo` can override static file lookup

## Dublin Core Metadata Table

```liquid
{% for key in site.data.metadata.fields %}
  {% assign value = page[key[0]] %}
  {% if value %}
    <tr><td>{{ key[1] }}</td><td>{{ value }}</td></tr>
  {% endif %}
{% endfor %}
```

Iterates `_data/metadata.yml`'s `fields` map. For each field, reads the matching `page` variable by key. Rows with blank values are suppressed.

## Includes / Inherits

- Inherits: `page.html` → `default.html`
- No child includes called

## Used By

All files in `_items/` with `layout: item` in front matter.

## Customization Notes

- **Adding metadata fields:** Add a new key-value pair to `_data/metadata.yml` under `fields:`. Then add the matching field to item front matter. No changes to `item.html` required.
- **Removing metadata fields:** Delete the entry from `_data/metadata.yml`. The table row disappears automatically.
- **YouTube parsing:** The layout handles both `youtu.be` short URLs and `youtube.com/watch?v=` long URLs. Other video platforms require adding a new parsing branch here.
- **Image lookup:** Static file search uses a substring match on the file path. If two items share an ID substring, both could match. Use distinct, collision-free item IDs.
- **Audio transcripts:** Transcript files must follow the naming convention `ItemID_Transcript.*` to be found by the static file search.
- **Featured image:** A second static file search runs below the content area to render a larger "featured" version of the item image. The same image resolution logic applies.
