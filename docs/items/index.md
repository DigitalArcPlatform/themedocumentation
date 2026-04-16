---
title: Items Folder
layout: default
nav_order: 4
---


# The "_items" Folder

```
├── _items/
│   └── YYYY-MM-DD-NNNN.md       ← item records (layout: item)
│       example: 2019-10-01-0003.md
```

Contains files that manage the display of the objects in a collection.

Any naming convention will work, and files will sort alphabetically.

We generally recommend naming conventions as follows
- for archieves: a YYYY-MM-DD-NNNN.md naming convention for date-based sorting
- for portfolios: a NN-TITLE.md naming convention (e.g. 01-MyProject.md) to control sorting for portfolio projects.

The documentation here uses the date-based archive naming convention.


# `_items/2019-10-01-0003.md`

Reference example of a complete item file — a physical object (hat) with category tags, contributor attribution, and descriptive body content.

## Role

A representative item record in the `_items/` Jekyll collection. Rendered by `_layouts/item.html`. Demonstrates the full range of available front matter fields, the standard filename convention, and the expected body content structure.

## Filename Convention

```
YYYY-MM-DD-NNNN.md
```

| Segment | Value | Purpose |
|---|---|---|
| `YYYY-MM-DD` | `2019-10-01` | Accession/entry date; controls sort order within the collection |
| `NNNN` | `0003` | Zero-padded sequence number within that date |

The full filename (without `.md`) becomes the **Item ID** (`2019-10-01-0003`). This ID is used by `item.html` and `_itembox.html` to search `site.static_files` for matching image, audio, and transcript assets.

## Front Matter

```yaml
layout: item
format: photo
title: Grateful Dead Hat
author: "IDAH Team"
contributor: "Drew H"
group: ""
creator: "Grateful Dead Productions"
externalurl: ""
embedurl: ""
creationdate: "ca. 2018"
type: "Physical Object"
shortdesc: "A turquoise strap-back hat with a Grateful Dead dancing bear on the front"
contributorquote: ""
categories: [ Clothing, Music ]
tags: [ ]
teammember: Andy Floyd
```

### Front Matter Field Reference

| Field | Type | Displayed In | Notes |
|---|---|---|---|
| `layout` | string | — | Must be `item` for the item layout |
| `format` | string | filter system (`data-formats`) | Object type; used by `_itembox.html` format filter |
| `title` | string | header band, card title, metadata table | Required |
| `author` | string | — | Maps to `site.data.authors` key; used if posts also exist in this collection |
| `contributor` | string | item card right column, metadata table | Person who donated or contributed the item |
| `group` | string | metadata table, group/stories layouts | Links item to a group page via `item.itemdescendant` match |
| `creator` | string | item card right column, metadata table | Original creator of the object |
| `externalurl` | string | item card right column | Link to item at an external archive or source |
| `embedurl` | string | item card left column | YouTube or embed URL; triggers video player |
| `creationdate` | string | metadata table | Date of original creation; free-form text |
| `type` | string | metadata table | Dublin Core type (e.g. "Physical Object", "Sound Recording") |
| `shortdesc` | string | item card, metadata table, `_itembox.html` excerpt | Brief one-sentence description |
| `contributorquote` | string | item card right column | Pull quote from the contributor |
| `categories` | array | filter buttons, metadata table | Content categories; drives `_itemlist.html` filter UI |
| `tags` | array | metadata table | Additional tags; not currently used in filter UI |
| `teammember` | string | item card right column, metadata table | Project team member who assisted with the item |

## Body Content Structure

The item body (below front matter) is rendered as `content` in `item.html` after the two-column card. Convention used in this example:

```markdown
## About This Item
[Scholarly/contextual description — connects object to primary and secondary sources]

## From the Contributor
[Personal context — contributor's own words or paraphrase about the object's significance]
```

This two-section structure is a convention, not enforced by the layout. Any Markdown is valid.

## Asset Lookup (driven by Item ID `2019-10-01-0003`)

| Asset Type | Expected Path Pattern | Fallback |
|---|---|---|
| Item image | `site.static_files` path containing `2019-10-01-0003` | `site.placeholderimg` |
| Audio file | `site.static_files` path containing `2019-10-01-0003.mp3` | audio player suppressed |
| Transcript | `site.static_files` path containing `2019-10-01-0003_Transcript` | transcript link suppressed |

## Filter System Participation

| Filter Type | Value | Source |
|---|---|---|
| Category filter | `Clothing`, `Music` | `categories` array |
| Format filter | `photo` | `format` field |

The `_itemlist.html` and `_itembox.html` includes read these values to populate filter buttons and set `data-*` attributes on cards.

## Customization Notes

- **New items:** Copy this file, rename using the `YYYY-MM-DD-NNNN` convention, and update all front matter fields. The Item ID in the filename drives all asset lookups automatically.
- **Images:** Place image files in the directory referenced by `site.urlimg`. Name them to include the Item ID (e.g. `2019-10-01-0003.jpg`) so the static file search finds them.
- **Empty fields:** Leave optional fields as `""` or `[]` rather than removing them entirely. Removing fields that `item.html` references won't break the page, but keeping them makes front matter self-documenting.
- **`group` vs `categories`:** `group` links the item to a `group.html` page via `item.itemdescendant`. `categories` powers the filter buttons on collection and stories pages. These are independent — an item can have both, either, or neither.
- **`format` naming:** Use consistent values across all items (e.g. always `photo`, not sometimes `Photo` or `photograph`). Inconsistent casing creates duplicate filter buttons.
