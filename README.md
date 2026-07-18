# Gu Liujie's Personal Website

A personal static site built with **GitHub Pages + Jekyll** (minima theme),
covering bio, blog, open-source projects, and a corner for fun interactive toys.

Live site: https://liujiegu.github.io

## Sections

- **Home** (`index.md`) — avatar hero, intro, and navigation to all sections
- **About** (`about.md`) — bio, education, and contact
- **Blog** (`blog.md` + `_posts/`) — Markdown articles
- **Projects** (`projects.md`) — showcase of public open-source work (helix, databuffer)
- **Something Interesting** (`something-interesting.md`) — small zero-dependency
  Canvas toys (starfield, random-walk K-line) embedded via `<iframe>`

## Local preview

```bash
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000

## Deploy

Deployment is handled by **GitHub Actions** (`.github/workflows/deploy.yml`):
every push to `main` builds the site with Jekyll and publishes it to GitHub Pages.
In **Settings → Pages**, Source is set to **GitHub Actions**.

> Note: the `github-pages` gem is intentionally omitted — it calls the GitHub
> API for repo metadata during build and fails in CI without auth. A plain
> Jekyll 4.x build is used instead.

## Directory structure

```
.
├── _config.yml                 # site title, author, nav, theme
├── Gemfile                     # dependencies (jekyll, minima)
├── index.md                    # homepage (avatar hero + nav)
├── about.md                    # bio
├── blog.md                     # post list
├── projects.md                 # project showcase
├── something-interesting.md    # fun toys entry
├── something-interesting/      # standalone HTML toys (starfield, kline)
├── assets/profile.png          # avatar
├── _posts/                     # YYYY-MM-DD-title.md
└── .github/workflows/deploy.yml
```
