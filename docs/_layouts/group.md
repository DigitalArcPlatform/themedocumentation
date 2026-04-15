---
title: group.html
layout: default
nav_order: 4
parent: "_Layouts" Folder"
---

# `_layouts/group.html`

Group page layout — displays a filtered subset of items that share a `folder` value, with an optional oral history sidebar.

***Currently not used***

## Role

Used for pages that aggregate related items under a named group (e.g. a single interview session or community collection). Looks up items whose `item.itemdescendant` field matches `page.folder`, renders each as an item card, and optionally shows an oral history sidebar if a matching entry exists in `site.oralhistories`.

## Front Matter

```yaml
layout: page
format: group
```

Extends `page` (which extends `default`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.folder` | page front matter | The group identifier; used to filter `site.items` and look up oral histories |
| `page.title` | page front matter | Passed through to `page.html` header band |
| `site.items` | Jekyll collection (`_items/`) | Full item list; filtered by `item.itemdescendant == page.folder` |
| `item.itemdescendant` | item front matter | Folder/group identifier that links an item to a group page |
| `site.oralhistories` | Jekyll collection (`_oralhistories/`) | Collection of oral history documents; filtered by `folder` field |
| `oralhistory.excerpt` | computed | First paragraph of the matched oral history document |
| `oralhistory.url` | Jekyll built-in | Link to the full oral history document |

## Layout Logic

1. `{% assign oralhistory = site.oralhistories | where: "folder", page.folder | first %}` — finds the first oral history with a matching `folder` value
2. If an oral history with an excerpt exists: renders a two-column layout (items + sidebar)
3. If no oral history: renders items in a single-column layout
4. Items loop: `{% for item in site.items %}{% if item.itemdescendant == page.folder %}` — includes `_itembox.html` for each match

## Includes / Inherits

- Inherits: `page.html` → `default.html`
- `{% include _itembox.html %}` — called inside the items loop (note: called as `itembox.html` without underscore prefix in some versions; verify actual filename)

## Used By

Any page with `layout: group` in front matter. Typically one page per group/folder.

## Customization Notes

- **`page.folder` key:** This value must exactly match both the `folder` field in `_oralhistories/` documents and the `itemdescendant` field in `_items/` documents. A typo in any one of these three places will silently break the group association.
- **Oral histories collection:** The `site.oralhistories` collection must be declared in `_config.yml` under `collections:` for Jekyll to expose it. If the collection is missing or empty, the sidebar simply doesn't render.
- **Item filtering:** Filtering is done in Liquid (not at build time). All items are iterated; only matching ones are rendered. For large collections, this is a performance consideration.
- **Sidebar content:** The sidebar shows `oralhistory.excerpt` (auto-generated first paragraph) and a link to the full document. To show more content, use `oralhistory.content` instead and apply a `truncatewords` filter.
