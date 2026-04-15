# DigitalArc Jekyll Theme — Technical Reference

Developer-facing reference for the DigitalArc Jekyll theme. Aimed at Jekyll-experienced users who want to customize or extend the theme after initial deployment.

For beginner setup, see the user guide. This document covers file structure, variable dependencies, and inter-file relationships.

---

## File Tree

```
.
├── _config.yml                   ← site-wide variables (not documented here)
│
├── _data/
│   ├── navigation.yml            ← nav menu items array
│   ├── authors.yml               ← author profile map (keyed by author ID)
│   └── metadata.yml              ← Dublin Core field labels for item pages
│
├── _includes/
│   ├── _head.html                ← <head> block (meta, CSS, JS, analytics)
│   ├── _header-and-nav.html      ← sticky nav bar and mobile menu
│   ├── _footer.html              ← footer (social, copyright, attribution)
│   ├── _itembox.html             ← single item card (called in loops)
│   ├── _itemlist.html            ← full filterable item grid
│   └── _postlist.html            ← blog post list
│
├── _layouts/
│   ├── default.html              ← root layout (head + nav + content + footer + JS)
│   ├── blank.html                ← bare pass-through (no wrapping HTML)
│   ├── page.html                 ← standard content page (dark header + body)
│   ├── post.html                 ← blog post (extends page)
│   ├── homepage.html             ← two-column hero page (extends default)
│   ├── collection.html           ← collection index (extends page; blog or items)
│   ├── group.html                ← grouped items + oral history sidebar (extends page)
│   ├── item.html                 ← individual item record (extends page)
│   └── stories.html              ← grouped stories with tag filters (extends page)
│
├── _items/
│   └── YYYY-MM-DD-NNNN.md       ← item records (layout: item)
│       example: 2019-10-01-0003.md
│
├── _posts/
│   └── YYYY-MM-DD-title.md      ← blog posts (layout: post)
│
├── _oralhistories/              ← oral history documents (referenced by group.html)
│
├── assets/
│   ├── css/main.css             ← compiled stylesheet
│   └── js/
│       ├── jquery.js
│       ├── what-input.js
│       ├── foundation.js
│       └── app.js               ← custom JS (filter show/hide logic)
│
└── pages/
    ├── index.md                  ← site root (layout: blank, fully custom HTML)
    ├── collection.md             ← collection index page (layout: collection)
    └── docs/                     ← this documentation folder
```

---

## Layout Inheritance Chain

```
default.html
├── blank.html          (parallel — does not extend default)
├── homepage.html       (extends default directly)
└── page.html
    ├── post.html
    ├── collection.html
    │   ├── _postlist.html  (included when URL contains "blog")
    │   └── _itemlist.html  (included otherwise)
    │       └── _itembox.html
    ├── group.html
    │   └── _itembox.html   (included in item loop)
    ├── item.html
    └── stories.html
        └── _itembox.html   (included in nested loops)
```

---

## Quick Reference: Files × Variables

### `_config.yml` variables and where they're used

| Variable | Used In |
|---|---|
| `site.title` | `_head.html`, `_header-and-nav.html`, `_footer.html`, `homepage.html`, `pages/index.md` |
| `site.subtitle` | `homepage.html` |
| `site.description` | `_footer.html`, `pages/collection.md` |
| `site.baseurl` | all layouts and includes |
| `site.urlimg` | `_footer.html`, `_itembox.html`, `_postlist.html`, `item.html`, `post.html`, `homepage.html` |
| `site.sitelogo` | `_footer.html`, `homepage.html` |
| `site.authorname` | `_footer.html` |
| `site.email` | `_footer.html`, `homepage.html` |
| `site.twitter` | `_footer.html`, `pages/index.md` |
| `site.instagram` | `_footer.html`, `pages/index.md` |
| `site.facebook` | `_footer.html`, `pages/index.md` |
| `site.github` | `_footer.html`, `pages/index.md` |
| `site.website` | `_footer.html`, `pages/index.md` |
| `site.keywords` | `_head.html` |
| `site.google_g4_analytics_id` | `_head.html` |
| `site.sitedate` | `default.html` (computes `SiteYear`) |
| `site.copyright_page` | `_footer.html` |
| `site.placeholderimg` | `_itembox.html` |

### Data files and where they're used

| Data File | Variable | Used In |
|---|---|---|
| `navigation.yml` | `site.data.navigation` | `_header-and-nav.html`, `pages/index.md` |
| `authors.yml` | `site.data.authors[post.author]` | `_postlist.html` |
| `metadata.yml` | `site.data.metadata.fields` | `item.html` |

### Collections and where they're used

| Collection | Variable | Used In |
|---|---|---|
| `_items/` | `site.items` | `_itemlist.html`, `_itembox.html`, `group.html`, `stories.html` |
| `_posts/` | `site.posts` | `_postlist.html` |
| `_oralhistories/` | `site.oralhistories` | `group.html` |
| all assets | `site.static_files` | `_itembox.html`, `item.html` |

---

## Documentation Files

Each source file is documented individually:

### `_includes/`
- [_head.html](_includes/_head.md)
- [_header-and-nav.html](_includes/_header-and-nav.md)
- [_footer.html](_includes/_footer.md)
- [_itembox.html](_includes/_itembox.md)
- [_itemlist.html](_includes/_itemlist.md)
- [_postlist.html](_includes/_postlist.md)

### `_layouts/`
- [default.html](_layouts/default.md)
- [blank.html](_layouts/blank.md)
- [page.html](_layouts/page.md)
- [post.html](_layouts/post.md)
- [homepage.html](_layouts/homepage.md)
- [collection.html](_layouts/collection.md)
- [group.html](_layouts/group.md)
- [item.html](_layouts/item.md)
- [stories.html](_layouts/stories.md)

### `_data/`
- [navigation.yml](_data/navigation.md)
- [authors.yml](_data/authors.md)
- [metadata.yml](_data/metadata.md)

### `pages/`
- [pages/index.md](pages/index.md)
- [pages/collection.md](pages/collection.md)

### `_items/`
- [2019-10-01-0003.md (annotated example)](_items/2019-10-01-0003.md)
