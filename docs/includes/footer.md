---
title: footer.html
layout: default
nav_order: 1
parent: Includes Folder
---

# `_includes/_footer.html`

Renders the site footer — social media links, logo, description, copyright year range, license badge, and framework attribution.

## Role

Included at the bottom of `default.html`, after `content` and before the JS `<script>` blocks. Visible on every page that uses the `default` layout chain.

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `site.twitter` | `_config.yml` | Twitter/X profile URL; icon link hidden if blank |
| `site.instagram` | `_config.yml` | Instagram profile URL; icon link hidden if blank |
| `site.facebook` | `_config.yml` | Facebook profile URL; icon link hidden if blank |
| `site.github` | `_config.yml` | GitHub profile URL; icon link hidden if blank |
| `site.website` | `_config.yml` | External website URL; icon link hidden if blank |
| `site.email` | `_config.yml` | Contact email; `mailto:` link hidden if blank |
| `site.urlimg` | `_config.yml` | Base path for image assets |
| `site.sitelogo` | `_config.yml` | Filename of the logo image shown in the footer avatar block |
| `site.title` | `_config.yml` | Site name displayed next to the logo |
| `site.authorname` | `_config.yml` | Author/organization name in footer credit line |
| `site.description` | `_config.yml` | Short site description displayed under the logo |
| `site.copyright_page` | `_config.yml` | URL of the full copyright/license page linked from the footer |
| `SiteYear` | computed in `default.html` | Year extracted from `site.sitedate`; used as range start |
| `NowYear` | computed in `default.html` | Current year; used as range end |

## Copyright Year Logic

`SiteYear` and `NowYear` are captured in `default.html` using `capture`. The footer conditionally displays a year range:

- If `SiteYear != NowYear`: renders `SiteYear – NowYear`
- If equal (launch year = current year): renders only `NowYear`

These variables must be set in `default.html` before this include is called.

## Includes / Inherits

None.

## Used By

- `_layouts/default.html` (only direct caller)
- Inherited by all layouts that extend `default`

## Customization Notes

- **Social links:** Each icon is individually conditional — set or remove the corresponding var in `_config.yml`. No changes to this file needed.
- **Logo:** Set `site.urlimg` + `site.sitelogo` in `_config.yml` to control the footer logo image.
- **License:** The Creative Commons BY-NC-SA 4.0 badge is hardcoded. To change the license, replace the badge `<img>` tags and the `href` on the surrounding link.
- **Copyright page:** Set `site.copyright_page` to the permalink of your copyright/terms page.
- **Attribution line:** The "DigitalArc Jekyll Theme by Kalani Craig" line is hardcoded at the bottom of the footer. Remove or edit it directly in this file.
