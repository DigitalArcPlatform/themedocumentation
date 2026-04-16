---
title: Layouts Folder
layout: default
nav_order: 2
has_children: true
---


# The "_Layouts" Folder

```
├── _layouts/
│   ├── blank.html                ← bare pass-through (no wrapping HTML)
│   ├── collection.html           ← collection index (extends page; blog or items)
│   ├── default.html              ← root layout (head + nav + content + footer + JS)
│   ├── group.html                ← grouped items + oral history sidebar (extends page)
│   ├── homepage.html             ← two-column hero page (extends default)
│   ├── item.html                 ← individual item record (extends page)
│   ├── page.html                 ← standard content page (dark header + body)
│   ├── post.html                 ← blog post (extends page)
│   └── stories.html              ← grouped stories with tag filters (extends page)
│
```

This folder contains layout definitions for the theme.

## Of interest:
- The `collection.html` layout controls the index of objects listed (the page with all of the item cards)
- The `item.html` layout controls the layout of an individual object. To change how metadata fields are displayed beyond the multi-language customzation available at `_data/metadata.yml`, some customization may be necessary on this page.
- The `default.html` layout is the most commonly used layout for user-defined pages in the ``/pages` folder.
