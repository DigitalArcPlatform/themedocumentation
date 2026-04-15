# `_includes/_itemlist.html`

Renders the full filterable item grid — category filter buttons, optional format checkboxes, and the item card grid.

## Role

Included by `collection.html` when the page URL does not contain `"blog"`. Iterates `site.items` twice: first to build unique filter lists, then to render item cards via `_itembox.html`. The filter UI is rendered above the grid; JavaScript in `app.js` handles show/hide behavior.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.items` | Jekyll collection (`_items/`) | Full list of items; iterated to build filter lists and render cards |
| `item.categories` | item front matter | Array; collected into `uniqueCategories` for filter buttons |
| `item.format` | item front matter | String; collected into `uniqueFormats` for format checkboxes |
| `item.title` | item front matter | Used in type-checking guard to skip malformed items |

## Filter Build Logic

**Categories (content-based filtering):**

Loops all items, pushes each category value into `uniqueCategories`, then deduplicates with `| uniq | sort`. Renders one filter button per unique category, plus an "All" button.

**Formats (object-type filtering):**

Same pattern into `uniqueFormats`. The format checkbox group is only rendered if more than one unique format exists — if all items share a single format, the checkbox UI is suppressed.

## Includes

- `{% include _itembox.html %}` — called once per item in the grid loop

## Used By

- `_layouts/collection.html` (conditional: only when URL does not contain `"blog"`)

## Customization Notes

- **Filter button labels:** Button text comes directly from the `categories` values in item front matter. Standardize category spelling across items in `_items/` to avoid duplicate buttons.
- **Format checkboxes:** The checkbox group is hidden when all items share one format. Add a second `format` value to any item to make the UI appear.
- **Grid columns:** The item grid uses `large-12` Foundation cell. Inner card columns are set in `_itembox.html`.
- **JavaScript dependency:** Filter show/hide is handled by `app.js`. The filter buttons set `data-filter` values; the grid items expose `data-categories` and `data-formats`. Both sides must use consistent values for filtering to work.
- **Performance:** This include iterates `site.items` twice (once for filter build, once for cards). For very large collections, consider pre-computing filter lists in a plugin or data file.
