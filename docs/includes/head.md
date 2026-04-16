---
title: head.html
layout: default
nav_order: 2
parent: Includes Folder
---

# `_includes/_head.html`

Renders the full `<head>` block — meta tags, CSS, JS, analytics, and SEO — included in every page via `default.html`.

## Role

Included once at the top of `default.html`. Everything that belongs in `<head>` lives here so that all layouts inherit it automatically through the `default` chain.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.title` | page front matter | Sets `<title>` and `<meta name="keywords">` |
| `site.title` | `_config.yml` | Appended to `<title>` as site name suffix |
| `page.keywords` | page front matter | Page-specific keywords in `<meta name="keywords">` |
| `site.keywords` | `_config.yml` | Site-wide fallback keywords appended to page keywords |
| `site.baseurl` | `_config.yml` | Prefix for the local `main.css` path |
| `site.google_g4_analytics_id` | `_config.yml` | Google Analytics 4 measurement ID; block is omitted if this var is blank |

## Includes / Inherits

- `{% seo %}` — Jekyll SEO Tag plugin; auto-generates Open Graph, Twitter Card, and canonical URL tags

## External Dependencies

- `main.css` at ` [ site.baseurl ] /assets/css/main.css`
- Font Awesome kit loaded from `https://kit.fontawesome.com/3f7330d0fa.js`
- Google Analytics 4 script (conditional on `site.google_g4_analytics_id`)

## Used By

- `_layouts/default.html` (only direct caller)
- Inherited by all layouts that extend `default`: `page`, `post`, `homepage`, `collection`, `group`, `item`, `stories`

## Customization Notes

- **Analytics:** Set `google_g4_analytics_id` in `_config.yml` to enable GA4. Leave blank to suppress the script entirely.
- **CSS:** Swap the `main.css` path to point to a custom stylesheet. Do not add a second `<link>` tag here without removing the original, or styles will conflict.
- **Font Awesome:** Replace the kit URL with your own kit ID from fontawesome.com if you need a different icon set or version.
- **Additional `<head>` tags:** Add them directly in this file — all pages inherit them automatically.
