# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start local dev server at http://localhost:4321
npm run build     # Build for production (output to dist/)
npm run preview   # Preview the production build locally
```

There are no tests or linters configured.

## Architecture

This is an [Astro](https://astro.build) static site deployed to GitHub Pages at `https://sequoiap.github.io`. Deployment happens automatically via `.github/workflows/deploy.yml` on every push to `master`.

### Pages

All pages live in `src/pages/` and compose `Header`, `Footer`, and `BaseHead` components directly (no shared page layout wrapper). The four main sections are:

- **`index.astro`** — homepage
- **`projects.astro`** — project cards; the list of projects is a plain TypeScript array defined in the frontmatter of the file itself
- **`resume.astro`** — resume; content is hardcoded directly in the file
- **`blog/index.astro`** + **`blog/[...slug].astro`** — blog listing and post pages, driven by the content collection

### Blog content collection

Blog posts are Markdown or MDX files in `src/content/blog/`. The collection schema is defined in `src/content.config.ts` and requires `title`, `description`, and `pubDate`; `updatedDate` and `heroImage` are optional. To add a new post, create a `.md` file in that directory with the appropriate frontmatter — no other changes needed.

### Global config

- `src/consts.ts` — `SITE_TITLE` and `SITE_DESCRIPTION` used across all pages
- `astro.config.mjs` — site URL, MDX and sitemap integrations
- `src/styles/global.css` — all global styles; uses CSS custom properties for theming (colors via `--accent`, `--gray`, etc.)
