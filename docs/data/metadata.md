---
title: metadata.yml
layout: default
nav_order: 2
parent: Data Folder
---

# `_data/metadata.yml`

Maps item front matter field names to human-readable display labels for the Dublin Core metadata table on item pages.

## Role

Consumed by `_layouts/item.html` to render the metadata table at the bottom of every item page. The file controls both which fields appear in the table and what label each field receives. Fields absent from this file are never shown in the table, regardless of whether they exist in item front matter.

## Data Structure

```yaml
fields:
  field_key: "Display Label"
  ...
```

| Field Key | Display Label | Notes |
|---|---|---|
| `title` | Title | |
| `creator` | Creator | |
| `contributor` | Contributor | |
| `creationdate` | Date | |
| `type` | Type | |
| `shortdesc` | Short Description | |
| `group` | Group | |
| `categories` | Categories | Array values are displayed as-is |
| `tags` | Tags | Array values are displayed as-is |
| `teammember` | Team Member | |
| `contributorquote` | Contributor Quote | |

## Lookup Pattern in `item.html`

```liquid
{% for key in site.data.metadata.fields %}
  {% assign value = page[key[0]] %}
  {% if value %}
    <tr><td> [ key[1] ] </td><td> [ value ] </td></tr>
  {% endif %}
{% endfor %}
```

- `key[0]` — the field key (e.g. `"creator"`)
- `key[1]` — the display label (e.g. `"Creator"`)
- `page[key[0]]` — reads the corresponding front matter field from the item page
- Rows where the value is blank or undefined are suppressed

## Used By

- `_layouts/item.html` — Dublin Core metadata table

## Customization Notes

- **Adding a field to the table:** Add a new `field_key: "Label"` line under `fields:`. Then add the matching field to item front matter in `_items/`. The table row appears automatically on rebuild.
- **Removing a field:** Delete the line from `fields:`. The field vanishes from all item pages immediately. The data in item front matter is unaffected.
- **Renaming a label:** Change the display label string. The field key and front matter field name are unchanged.
- **Field order:** The table renders fields in the order they appear in this file. Reorder lines here to reorder table rows.
- **Field key naming:** Keys must exactly match the front matter field names in item files. Keys are case-sensitive.
- **Array fields:** `categories` and `tags` are arrays in item front matter. The template renders their raw Liquid output (e.g. `ClothingMusic` without separator). To format arrays as comma-separated lists, modify the table loop in `item.html` to apply `| join: ", "` for array values.
