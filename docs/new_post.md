# Adding New Posts to the Site

This site is built with [Hugo](https://gohugo.io) using the `hugo-blog-awesome` theme. Blog posts and project entries are both Hugo **page bundles** — a directory containing an `index.md` file, with optional image assets alongside it.

---

## Quick Start

```bash
# Create a new blog post
mkdir -p content/blog/my-post-title
# Then create content/blog/my-post-title/index.md (see template below)
https://www.linkedin.com/in/peter-aneke/
# Create a new project entry
mkdir -p content/projects/my-project
# Then create content/projects/my-project/index.md (same format as blog)
```

---

## Directory Structure
```
content/blog/<slug>/index.md        # Blog post content (required)
content/blog/<slug>/image.jpg       # Optional image assets

content/projects/<slug>/index.md    # Project entry content (required)
content/projects/<slug>/image.jpg   # Optional image assets
```

---

## Frontmatter Reference

Every `index.md` file must start with YAML frontmatter enclosed in `---` delimiters.

### Required Fields

| Field | Description |
|-------|-------------|
| `title` | Post or project title. Appears in page `<title>`, headings, and post cards. |

### Recommended Fields

| Field | Description |
|-------|-------------|
| `date` | Publication date in `YYYY-MM-DD` format. Controls sort order (most recent first). |
| `description` | Short summary for SEO meta tags and previews. Falls back to the site-wide description if omitted. |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `author` | string | Author name displayed on the post. Defaults to the site author. |
| `tags` | array | Taxonomy tags, e.g. `["go", "web"]`. |
| `draft` | boolean | If `true`, the post is excluded from published output. |
| `isStarred` | boolean | If `true`, shows a star icon next to the title in post listings. |
| `image` | string | Custom `og:image` URL/path for social sharing previews. |
| `math` | boolean | If `true`, loads KaTeX on this page for math typesetting. |
| `toc` | boolean | Override the global table-of-contents setting for this page. |
| `tocOpen` | boolean | If `true`, the table of contents is expanded by default. |
| `category` | string | Schema.org article section metadata. |

---

## Full Template

### Blog Post

Create `content/blog/<url-slug>/index.md`:

```yaml
---
title: Your Post Title
date: 2025-06-29
description: A short description for SEO and post previews.
author: Your Name
tags:
  - example
  - tutorial
draft: false
isStarred: false
---

Write your markdown content here.

Use `<!--more-->` to split the summary shown in listings
from the full article content.

## A Heading

More content with **bold**, *italic*, `code`, and [links](https://example.com).

```python
print("Code blocks work too")
```

![Image alt text](filename.jpg)
```

### Project Entry

Create `content/projects/<url-slug>/index.md` using the **exact same format** as blog posts:

```yaml
---
title: My Project
date: 2025-06-29
description: A description of the project.
author: Your Name
tags:
  - open-source
  - go
draft: false
isStarred: false
---

Project details, screenshots, links, and any other content.
```

---

## Images

Place images in the **same directory** as the `index.md` file and reference them with a relative path:

```
content/blog/my-post/
├── index.md
├── screenshot.jpg
└── diagram.png
```

```markdown
![Screenshot](screenshot.jpg)
![Architecture diagram](diagram.png)
```

External image URLs also work:

```markdown
![Random photo](https://source.unsplash.com/random/600x400/?tech)
```

---

## Content Summary (`<!--more-->`)

Place `<!--more-->` in the body of the post to define where the summary ends. Everything before `<!--more-->` becomes the preview text shown in blog listings and RSS feeds.

```markdown
This sentence appears in the summary.

<!--more-->

This content only appears on the full post page.
```

---

## Tags

Tags are defined as a YAML array in frontmatter:

```yaml
tags:
  - go
  - web
  - performance
```

Tags appear on the post page and create filterable taxonomy pages at `/tags/<tagname>/`. Use consistent casing across posts to avoid duplicate tag pages.

---

## Draft Posts

Set `draft: true` in frontmatter to prevent a post from being published. Draft posts are excluded from the site output when running `hugo server` or building for production. Useful for works-in-progress.

```yaml
draft: true
```

To preview drafts locally, run:

```bash
hugo server -D
```

---

## Table of Contents

The site has a global table of contents enabled (`toc = true` in `hugo.toml`). It is collapsed by default (`tocOpen = false`).

Override per-post:

```yaml
toc: false       # Disable ToC for this post
tocOpen: true    # Expand ToC by default for this post
```

---

## Math (KaTeX)

```yaml
math: true
```

Enables KaTeX rendering on the page. Use standard LaTeX math delimiters:

```markdown
Inline: $E = mc^2$

Block:
$$
\int_a^b f(x) \, dx
$$
```

---

## Starred Posts

```yaml
isStarred: true
```

Adds a star icon next to the post title in listings. Useful for highlighting notable posts or pinned projects.

---

## Routing (URLs)

The directory path under `content/` maps directly to the published URL:

| Content Path | Published URL |
|---|---|
| `content/blog/my-post/index.md` | `/blog/my-post/` |
| `content/blog/2025/update/index.md` | `/blog/2025/update/` |
| `content/projects/awesome-app/index.md` | `/projects/awesome-app/` |

Choose URL-friendly slugs: lowercase, hyphens for spaces, no special characters.

---

## Navigation

Blog and projects are linked in the main navigation menu (configured in `hugo.toml`):

| Menu Item | URL |
|---|---|
| Home | `/` |
| Blog | `/blog/` |
| Projects | `/projects/` |
| About | `/about/` |

No additional configuration is needed when adding posts or projects — they appear automatically on their respective list pages.

---

## Homepage Visibility

Only blog posts appear on the home page (configured via `mainSections = ['blog']` in `hugo.toml`). Project entries appear on the `/projects/` list page but not on the home page.

To change this, edit the `mainSections` array in `hugo.toml`:

```toml
mainSections = ['blog']              # Current: only blog on homepage
mainSections = ['blog', 'projects']  # Show both blog and projects on homepage
```

---

## Local Preview

Start the Hugo development server:

```bash
hugo server
```

The site is served at `http://localhost:1313/`. Changes are live-reloaded automatically. Draft posts are excluded by default — use `hugo server -D` to include them.

---

## Build & Deploy

The site builds automatically via GitHub Actions on every push to `main`. The workflow is at `.github/workflows/hugo.yaml`. It:

1. Checks out the repository (with theme submodule)
2. Runs `hugo --minify` to build the site
3. Publishes to GitHub Pages

No manual build step is required. Push to `main` and the site updates within a few minutes.

---

## Checklist for a New Entry

- [ ] Created directory: `content/blog/<slug>/` or `content/projects/<slug>/`
- [ ] Created `index.md` with `title`, `date`, and `description` frontmatter
- [ ] Set `draft: false` when ready to publish
- [ ] Added tags if applicable
- [ ] Placed images in the same directory (if any)
- [ ] Referenced images with relative paths (`![alt](filename.jpg)`)
- [ ] Tested locally with `hugo server`
- [ ] Committed and pushed to `main`
