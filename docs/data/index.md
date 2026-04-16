---
title: Data Folder
layout: default
nav_order: 5
has_children: true
---


# The "_Layouts" Folder

```
├── _includes/
│   ├── _head.html                ← <head> block (meta, CSS, JS, analytics)
│   ├── _header-and-nav.html      ← sticky nav bar and mobile menu
│   ├── _footer.html              ← footer (social, copyright, attribution)
│   ├── _itembox.html             ← single item card (called in loops)
│   ├── _itemlist.html            ← full filterable item grid
│   └── _postlist.html            ← blog post list
```

This folder contains include files that make files in the Layouts folder more efficient

## Of interest:
- The `itembox.html` include file lays out each individual item card in the collection.html layout
- The `itemlist.html` include file manages the filtering for the item grid in the collection.html layout
- The `default.html` layout is the most commonly used layout for user-defined pages in the ``/pages` folder.
