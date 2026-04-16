---
title: postlist.html
layout: default
nav_order: 6
parent: Includes Folder
---

# `_includes/_postlist.html`

Renders a list of blog posts — thumbnail, title, author attribution, date, and truncated excerpt.

## Role

Included by `collection.html` when the page URL contains `"blog"`. Iterates `site.posts` (Jekyll's built-in posts collection, sourced from `_posts/`) and outputs one list entry per post.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.posts` | Jekyll built-in | All posts from `_posts/`, reverse-chronological by default |
| `post.image` | post front matter | Optional thumbnail image filename; block is suppressed if blank |
| `post.title` | post front matter | Post heading and link text |
| `post.url` | Jekyll built-in | Link href for title and "read more" |
| `post.author` | post front matter | Key used to look up author data in `site.data.authors` |
| `post.date` | post front matter / filename | Formatted as `%d %B %Y` (e.g. `01 January 2024`) |
| `post.excerpt` | Jekyll built-in | Auto-generated from first paragraph; stripped of HTML and truncated to 30 words |
| `site.baseurl` | `_config.yml` | Prefixes image src paths |
| `site.urlimg` | `_config.yml` | Base image directory path |
| `site.data.authors[post.author]` | `_data/authors.yml` | Author object; provides `author.name` and `author.website` |

## Author Lookup

```liquid
assign author = site.data.authors[post.author]
```

The `post.author` value in front matter must exactly match a key in `_data/authors.yml`. If the key is not found, the author block renders without a name or link.

Author website link is conditional:

```liquid
if author.website
	<a href=" [ author.website ] "> [ author.name ] </a>
endif
```

## Includes / Inherits

None.

## Used By

- `_layouts/collection.html` (conditional: only when page URL contains `"blog"`)

## Customization Notes

- **Author data:** Add new authors to `_data/authors.yml` using the same key format. The key must match exactly what you put in `post.author` in the post's front matter.
- **Excerpt length:** `truncatewords:30` is hardcoded. Adjust the integer to change excerpt length.
- **Date format:** `%d %B %Y` outputs day-month-year. Change the format string to match your locale preference.
- **Post image:** Set `image` in a post's front matter to display a thumbnail. The path is relative to `site.urlimg`. Leave `image` blank to suppress the thumbnail entirely.
- **Sort order:** `site.posts` is always reverse-chronological. To change sort order, use a `sort` or `reverse` filter on the loop.
