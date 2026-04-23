<p align="center">
  <img src="public/favicon.svg" alt="Wimpy Dev logo" width="96" height="96">
</p>

# Wimpy Dev

Source for [blog.wimpy.dev](https://blog.wimpy.dev), personal blog built with Astro and deployed with Cloudflare.

## Highlights

- Astro 6 site with Markdown and MDX content collections
- Blog listing and post pages generated from `src/content/blog/`
- Built-in RSS feed and sitemap generation
- Cloudflare adapter and Wrangler config for deployment
- `mise`-managed setup, checks, and CI workflow

## Tech stack

- [Astro](https://astro.build/)
- TypeScript
- `@astrojs/mdx`, `@astrojs/rss`, `@astrojs/sitemap`
- Cloudflare Workers via `@astrojs/cloudflare`
- `pnpm`, `mise`, and VitePlus

## Getting started

### Prerequisites

- [`mise`](https://mise.jdx.dev/)

### Install dependencies

```bash
mise run setup
```

### Start local development server

```bash
pnpm dev
```

### Build production output

```bash
mise run build
```

### Run project checks

```bash
mise run check
```

## Writing posts

Add blog entries in `src/content/blog/` as `.md` or `.mdx` files.

Each post follows schema from `src/content.config.ts`:

```yaml
title: My post title
description: Short summary for cards and metadata
pubDate: 2026-04-23
updatedDate: 2026-04-24 # optional
heroImage: ./cover.jpg # optional
```

Site automatically:

- sorts posts newest-first on `/blog`
- builds individual post pages from collection slugs
- publishes RSS feed at `/rss.xml`

> [!NOTE]
> Repository still contains starter content, including placeholder homepage copy and `src/content/blog/demo-post.md`.

## Project layout

```text
.
├── src/
│   ├── components/      # Shared Astro components
│   ├── content/blog/    # Markdown and MDX blog posts
│   ├── layouts/         # Post layout
│   ├── pages/           # Route entrypoints
│   └── styles/          # Global styles
├── public/              # Static assets
├── .github/workflows/   # CI
├── astro.config.mjs     # Astro config and Cloudflare adapter
├── mise.toml            # Tooling and task runner config
└── wrangler.jsonc       # Cloudflare runtime config
```

## Deployment

Production builds target Cloudflare through Astro's Cloudflare adapter. CI runs on pushes to `main`, pull requests, and tags, and uses:

```bash
mise run setup
mise run check
```

If you use dev containers, `.devcontainer/devcontainer.json` is already configured for this repo.
