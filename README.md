# Hugo Icon Pack: Lucide

A Hugo module that ships the full Lucide SVG icon set and provides ready-to-use rendering helpers for:

- **Markdown content** (via shortcode)
- **Layout templates** (via partial)

This module is designed to be mounted into your site and then used anywhere in your content or templates.

---

## Features

- Includes Lucide icons as Hugo assets under `assets/icons/lucide/*.svg`.
- Provides a shortcode: `lucide`.
- Provides a partial: `lucide.html`.
- Uses SVG `<symbol>` + `<use>` output for efficient repeated icon use on a page.

---

## Installation

Add the module to your Hugo site:

```bash
go get github.com/davidsneighbour/hugo-icon-pack-lucide
```

Then import it in your Hugo configuration:

```toml
[module]
  [[module.imports]]
    path = "github.com/davidsneighbour/hugo-icon-pack-lucide"
```

> This module already defines the required mounts for `assets` and `layouts`.

---

## Find Icon Names

Search the Lucide icon catalog here:

- https://lucide.dev/icons/

Use the icon slug from that page (for example: `chevron-right`).

---

## Usage in Markdown (shortcode)

Use the `lucide` shortcode in content files:

```markdown
{{< lucide icon="chevron-right" >}}
```

With additional options:

```markdown
{{< lucide icon="chevron-right" width="24" height="24" class="text-primary" >}}
```

### Shortcode parameters

- `icon` (required): Lucide icon name.
- `width` (optional): width of the SVG, default `24`.
- `height` (optional): height of the SVG, default `24`.
- `class` (optional): custom CSS classes added to the rendered `<svg>`.
- `type` (optional): icon pack type, default `lucide`.

---

## Usage in Layout Files (partial)

Use the partial from templates, partials, list/single layouts, etc.:

```go-html-template
{{ partial "lucide.html" (dict "icon" "chevron-right") }}
```

With additional options:

```go-html-template
{{ partial "lucide.html" (dict "icon" "chevron-right" "width" 24 "height" 24 "class" "text-primary") }}
```

### Partial parameters

- `icon` (required): Lucide icon name.
- `width` (optional): width of the SVG, default `20`.
- `height` (optional): height of the SVG, default `20`.
- `class` (optional): custom CSS classes.
- `type` (optional): icon pack type, default `lucide`.

---

## Rendered Markup

The partial renders a wrapper and SVG use reference similar to:

```html
<span class="icon--lucide icon--chevron-right">
  <svg width="24" height="24" class="icon icon-chevron-right">
    <use href="#chevron-right"></use>
  </svg>
</span>
```

On first use per page, the icon symbol definition is injected; subsequent uses reuse it.

---

## Notes / Compatibility

- Requires Hugo with module support enabled.
- If an icon name does not exist, no symbol content is available for that icon.
- Width/height can be controlled per call; additional styling should be done in your own CSS.

---

## Development / Maintenance

This repository stores generated icon SVG assets from Lucide.

Potential maintenance tasks when updating Lucide versions:

- Refresh `assets/icons/lucide/*.svg` from the upstream release.
- Run a quick grep for renamed/deprecated icon slugs.
- Validate template references against existing icon names.
