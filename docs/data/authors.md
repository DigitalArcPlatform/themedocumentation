---
title: authors.yml
layout: default
nav_order: 1
parent: Data Folder
---


# `_data/authors.yml`

Maps author keys to author profile data, used to display attribution on blog post list entries.

## Role

Looked up in `_postlist.html` using the `post.author` front matter value as a key. Provides the author's display name, website, and other profile fields for rendering post attribution.

## Data Structure

Map of author objects keyed by author identifier string:

```yaml
author-key:
  name: "Display Name"
  website: https://example.com
  twitter: https://twitter.com/handle
  github: https://github.com/handle
  bio: "Short author bio"
  image: https://example.com/photo.jpg
```

| Field | Type | Used In | Purpose |
|---|---|---|---|
| `name` | string | `_postlist.html` | Displayed as author attribution text |
| `website` | string | `_postlist.html` | Wraps `name` in a link if present; suppressed if blank |
| `twitter` | string | not currently rendered | Author Twitter/X profile |
| `github` | string | not currently rendered | Author GitHub profile |
| `bio` | string | not currently rendered | Short biography |
| `image` | string | not currently rendered | Author photo URL |

## Lookup Pattern

```liquid
{% assign author = site.data.authors[post.author] %}
```

`post.author` in a post's front matter must exactly match a key in this file (e.g. `author: kalani-craig` → key `kalani-craig:`).

## Used By

- `_includes/_postlist.html` — author name and website link in post list entries

## Customization Notes

- **Adding an author:** Add a new top-level key (use `kebab-case` to match Jekyll convention). The key must exactly match what you put in `post.author` in post front matter.
- **Key format:** Keys are case-sensitive. `Kalani-Craig` and `kalani-craig` are different keys.
- **Unused fields:** `twitter`, `github`, `bio`, and `image` are in the data structure but not rendered by any current template. They are available for customization if you extend `_postlist.html` or other templates.
- **Missing author:** If `post.author` references a key that doesn't exist in this file, `author` will be undefined and `_postlist.html` will silently render no author name or link.
