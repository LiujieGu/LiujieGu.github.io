---
layout: post
title:  "Building This Site: My Personal Website Workflow"
date:   2026-07-18 12:00:00 +0800
categories: meta tutorial
---

When I decided to set up a personal website, I wanted three things: a place for
my bio, a blog, and a corner for fun side projects — all free to host and trivial
to update. This post walks through the exact workflow behind this site, in case
you want to build one too.

## Why GitHub Pages + Jekyll

- **Free hosting** on GitHub's infrastructure.
- **No build step required** if you use the default Jekyll pipeline, though I
  opted into GitHub Actions for more control.
- **Write in Markdown**, commit with git, and the site updates itself.
- Perfect fit for a researcher/engineer who lives in a terminal anyway.

## The Stack

| Layer        | Choice                | Why                                  |
|--------------|-----------------------|--------------------------------------|
| Hosting      | GitHub Pages          | Free, tied to the repo               |
| Generator    | Jekyll 4.x            | Markdown → static site               |
| Theme        | minima                | Clean, minimal, easy to extend       |
| CI/CD        | GitHub Actions        | Reproducible builds, no local Ruby   |
| Domain       | `<user>.github.io`    | Zero config, free                   |

## Repository Setup

Create a repo named exactly `<your-github-username>.github.io`. GitHub maps this
name to the user page automatically.

```bash
git init
git add -A
git commit -m "Initial commit"
git remote add origin git@github.com:<user>/<user>.github.io.git
git push -u origin main
```

## The Jekyll Scaffold

A minimal Jekyll site is just a handful of files:

```
.
├── _config.yml          # site title, author, nav, theme
├── Gemfile              # dependencies (jekyll, minima)
├── index.md             # homepage
├── about.md             # bio
├── blog.md              # post list
├── projects.md          # project showcase
├── something-interesting.md
├── _posts/              # YYYY-MM-DD-title.md
└── .github/workflows/deploy.yml
```

The `_config.yml` drives most of the site. Navigation lives in `header_pages`:

```yaml
title: Gu Liujie
author: Gu Liujie
theme: minima
header_pages:
  - about.md
  - blog.md
  - projects.md
  - something-interesting.md
```

## Deploying with GitHub Actions

I use a workflow that builds the site and publishes the artifact to GitHub
Pages. Key point: **drop the `github-pages` gem** — it tries to call the GitHub
API for repo metadata during build and fails in CI without auth. A plain Jekyll
build works fine.

```yaml
name: Deploy Jekyll site to Pages
on:
  push:
    branches: ["main"]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true
      - uses: actions/configure-pages@v5
      - run: bundle exec jekyll build
      - uses: actions/upload-pages-artifact@v3
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
    steps:
      - uses: actions/deploy-pages@v4
```

In **Settings → Pages**, set Source to **GitHub Actions**. Every push to `main`
now triggers a fresh build and deploy.

### Deploy flow

```
   local edit            git push            GitHub Actions                GitHub Pages
  ┌──────────┐         ┌──────────┐       ┌─────────────────┐          ┌──────────────┐
  │ .md/.html│ ──push──▶│  main    │──────▶│ 1. checkout     │          │              │
  │  changes │         │  branch  │       │ 2. setup Ruby   │──build──▶│ static site  │
  └──────────┘         └──────────┘       │ 3. jekyll build │          │  served at   │
                                          │ 4. upload artifact│         │ <user>.github│
                                          │ 5. deploy-pages  │──deploy─▶│ .io          │
                                          └─────────────────┘          └──────┬───────┘
                                                                               │
                                                          visitor ◀────────────┘
                                                          https://<user>.github.io
```

Each push runs the pipeline end-to-end: build the static site, upload it as a
Pages artifact, and publish. No local Ruby install required.

## Writing a Post

Just drop a Markdown file into `_posts/` with the right name:

```bash
# _posts/2026-07-18-my-first-post.md
---
layout: post
title:  "My First Post"
date:   2026-07-18 12:00:00 +0800
categories: jekyll update
---
Write your content here in Markdown.
```

## Fun Extras

The "Something Interesting" page embeds small zero-dependency Canvas toys
(starfield, a random-walk K-line) via plain `<iframe>` — no framework needed.
The Projects page is a simple card grid. Both are just static HTML/CSS.

## The Daily Loop

1. Edit Markdown or HTML.
2. `git commit -am "..." && git push`.
3. Wait ~30s, refresh the live site.

That's the whole workflow — no servers to manage, no database, no bill. If you
want the exact files, they're all in the repo.
