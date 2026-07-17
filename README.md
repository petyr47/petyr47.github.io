# Peter Aneke — Personal Site

Personal website and blog, built with [Hugo](https://gohugo.io) and the
[`hugo-blog-awesome`](https://github.com/hugo-sid/hugo-blog-awesome) theme.
Deployed automatically to GitHub Pages via GitHub Actions.

## Requirements

- Hugo **extended** ≥ 0.163.1 (for SCSS support)
- Git (with submodule support)

## Local development

```bash
# clone with the theme submodule
git clone --recurse-submodules <repo-url>
cd personalwebsite

# start the dev server (excludes drafts)
hugo server

# include drafts
hugo server -D
```

The site is served at `http://localhost:1313/` with live reload.

## Repository structure

```
content/        Blog posts, project entries, and pages (page bundles)
assets/         Static assets processed by Hugo (avatar, SCSS)
layouts/        Theme overrides (partials, RSS)
themes/         hugo-blog-awesome (git submodule)
docs/           Guides for adding new content
hugo.toml       Site configuration
.github/        CI workflow (Hugo build + Pages deploy)
```

## Adding content

Blog posts and project entries are both Hugo **page bundles**: a directory under
`content/` containing an `index.md` file, with optional images alongside it.

- Blog: `content/blog/<slug>/index.md` → published at `/blog/<slug>/`
- Projects: `content/projects/<slug>/index.md` → published at `/projects/<slug>/`

See [`docs/new_post.md`](docs/new_post.md) for a copy-paste template and the
full frontmatter reference, and [`docs/project_template.md`](docs/project_template.md)
for a starter project entry.

## Deployment

Every push to `main` triggers `.github/workflows/hugo.yaml`, which builds the
site with `hugo --minify` and publishes to GitHub Pages. No manual build step.