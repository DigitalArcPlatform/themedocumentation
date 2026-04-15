---
title: Index.md
layout: default
nav_order: 1
parent: Pages Folder
---

# `pages/index.md`

Theme landing/about page — a fully self-contained HTML page using `layout: blank` that implements its own nav, hero, content sections, and footer.

## Role

The root URL (`/`) of a site using this theme. Unlike all other pages, this file does not use the standard includes or layout chain. Instead it manually duplicates the navigation loop, header, footer, and script blocks to achieve a custom design that differs from the standard `page` layout.

## Front Matter

```yaml
layout: blank
title: DigitalArc Jekyll Theme
permalink: /
```

| Field | Value | Purpose |
|---|---|---|
| `layout` | `blank` | Passes content through with no wrapping HTML |
| `title` | DigitalArc Jekyll Theme | Browser tab title (used in `<title>` tag, which is defined inline in this file) |
| `permalink` | `/` | Serves the page at the site root |

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.baseurl` | `_config.yml` | Prefixes all internal asset and link paths |
| `site.urlimg` | `_config.yml` | Base path for images |
| `site.title` | `_config.yml` | Displayed in nav bar and hero section |
| `site.sitelogo` | `_config.yml` | Logo image filename shown in page body |
| `site.data.navigation` | `_data/navigation.yml` | Nav items; looped manually (not via `_header-and-nav.html`) |
| `site.twitter` | `_config.yml` | Footer social link |
| `site.instagram` | `_config.yml` | Footer social link |
| `site.facebook` | `_config.yml` | Footer social link |
| `site.github` | `_config.yml` | Footer social link |
| `site.website` | `_config.yml` | Footer social link |
| `site.email` | `_config.yml` | Footer contact link |
| `site.authorname` | `_config.yml` | Footer credit line |
| `site.description` | `_config.yml` | Footer description text |
| `site.copyright_page` | `_config.yml` | Footer copyright page link |
| `SiteYear` / `NowYear` | computed inline | Copyright year range (same logic as `default.html`) |

## Layout Structure

This file is a complete standalone HTML document:

```
<!DOCTYPE html>
<head> ... </head>
<body>
  [sticky nav — manual loop of site.data.navigation]
  [hero section — logo, tagline]
  [about section — who is it for, screenshot]
  [origin story section]
  [footer — social links, copyright, attribution]
  [scripts — jQuery, Foundation, app.js]
</body>
```

## Includes / Inherits

None. All structural elements are inline.

## Used By

Nothing depends on this file. It is a standalone page.

## Customization Notes

- **Layout divergence:** This page does not use `_includes/_header-and-nav.html` or `_includes/_footer.html`. Changes to those files do not automatically apply here. If you update the nav or footer includes, you must manually mirror those changes in this file.
- **Nav sync:** The navigation loop here reads from `site.data.navigation` just like the standard include, so adding/removing nav items in `_data/navigation.yml` does update this page — but nav markup differences (classes, HTML structure) will not match the standard nav.
- **Custom colors:** Section background colors (`#D3EAEE`, `#FCF0EE`, `#004042`) are set via inline `style` attributes. Move these to `main.css` if you want them maintainable outside this file.
- **Scripts:** jQuery, Foundation JS, and `app.js` are included inline at the bottom of this file, in the same order as `default.html`. Keep this order consistent if you add scripts.
- **When to switch to standard layout:** If you want this page to use the standard header/footer/nav, change `layout: blank` to `layout: homepage` and remove all the manually duplicated structural HTML. This is the recommended approach for sites that don't need the custom landing design.



