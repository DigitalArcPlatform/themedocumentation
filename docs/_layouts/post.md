# `_layouts/post.html`

Blog post layout — inherits the `page` header structure, adds a "News & Updates" label, and optionally floats a post image right of the body text.

## Role

Used by all files in `_posts/`. Renders a dark header band labeled "News & Updates" with the post title, then the post body. If the post has an `image` field, a thumbnail is floated to the right of the content.

## Front Matter

```yaml
layout: page
format: post
```

Extends `page` (which extends `default`).

## Variables Used

| Variable | Source | Purpose |
|---|---|---|
| `page.title` | post front matter | Displayed in the dark header band |
| `page.image` | post front matter | Optional thumbnail image filename; floated right if present |
| `site.baseurl` | `_config.yml` | Prefixes the image `src` path |
| `site.urlimg` | `_config.yml` | Base directory for post images |

## Image Handling

```liquid
{% if page.image %}
  <img class="article-image float-right thumbnail" src="{{ site.baseurl }}{{ site.urlimg }}{{ page.image }}">
{% endif %}
```

The image block is suppressed entirely when `image` is blank. Image path is `site.baseurl + site.urlimg + page.image`.

## Includes / Inherits

- Inherits: `page.html` → `default.html`
- `{{ content }}` — the post's Markdown body

## Used By

Any file in `_posts/` that specifies `layout: post`.

## Customization Notes

- **Section label:** "News & Updates" is hardcoded in the header band. Edit it directly in this file to change the section name for all posts.
- **Image placement:** The `float-right` class is Foundation-based. To change image placement (e.g. float left, full-width above content), edit the `class` attribute on the `<img>` tag.
- **Image path:** Post images must live under the path formed by `site.urlimg`. Set `site.urlimg` in `_config.yml` to match your image directory structure.
- **Per-post image size:** Image sizing is controlled by CSS classes (`article-image`, `thumbnail`). Override these in your stylesheet rather than adding inline styles here.
