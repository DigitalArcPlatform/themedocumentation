---
title: stories.html
layout: default
nav_order: 9
parent: Layouts Folder

# `_layouts/stories.html`

Stories/grouped collection layout — aggregates items by `group`, renders tag-based filter buttons, and displays items under their group headings.

## Role

Used for pages that present items organized into named groups (stories), with cross-group tag filtering. Unlike `collection.html` which shows all items in a flat filterable grid, `stories.html` groups items under subheadings. Filter buttons operate across all groups simultaneously.

## Front Matter

```yaml
layout: page
format: stories
```

Extends `page` (which extends `default`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.items` | Jekyll collection (`_items/`) | Full item list; iterated to build group and tag lists, then iterated again for display |
| `item.group` | item front matter | Group name; only items with a non-empty `group` value are included |
| `item.categories` | item front matter | Array; collected into `uniquetags` for filter buttons |
| `item.title` | item front matter | Used as guard to skip malformed items |

## Filter Build Logic

Two passes over `site.items`:

**Pass 1 — Build group and tag lists:**
```liquid
{% for item in site.items %}
  {% if item.group %}
    {% unless grouplist contains item.group %}...{% endunless %}
    ...collect uniquetags from item.categories...
  {% endif %}
{% endfor %}
```

Produces:
- `uniquegroups` — sorted, deduplicated list of group names
- `uniquetags` — sorted, deduplicated list of category values across all grouped items

**Pass 2 — Render:**
- Filter button row: "All" + one button per unique tag
- For each group in `uniquegroups`: H2 subheading, then loop items matching that group, calling `_itembox.html` for each

## Includes / Inherits

- Inherits: `page.html` → `default.html`
- `{% include _itembox.html %}` — called inside nested group + item loops

## Used By

Any page with `layout: stories` in front matter.

## Customization Notes

- **Items without a group:** Items where `item.group` is blank are silently excluded from this layout. They will not appear in any group heading or in the "All" filter view.
- **Group heading order:** Groups appear in the order determined by `uniquegroups` (sorted alphabetically by default). To control display order, either rename groups with a sort prefix or override the sort in Liquid.
- **Tag filter scope:** The tag filter buttons use the same `data-categories` attributes as `_itembox.html` cards. The JavaScript filter works across all groups simultaneously — filtering does not respect group boundaries.
- **Difference from `collection.html`:** `collection.html` → flat grid, format + category filters. `stories.html` → grouped display, category-only (tag) filters. Use `stories` when group organization matters; use `collection` for flat browsing.
- **Empty groups:** If all items in a group are filtered out by tag selection, the group H2 heading remains visible. Add JavaScript logic in `app.js` to hide empty group headings if desired.
