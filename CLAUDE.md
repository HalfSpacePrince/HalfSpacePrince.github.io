# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal portfolio website for a football performance analyst & scout, built with [Quarto](https://quarto.org). Content is authored in `.qmd` (Quarto Markdown) files and rendered to a static HTML site. There is no application code, test suite, or package manager — the "build" is Quarto rendering markdown to HTML.

## Commands

- `quarto preview` — Live-reloading dev server (watches `.qmd` files, rebuilds on save). Serves on a local port, e.g. `http://localhost:7168/`.
- `quarto render` — One-off full build of the site into `docs/`.

Requires the `quarto` CLI (installed at `/Applications/quarto/bin/quarto`).

## Deployment

The site is published via **GitHub Pages serving from the `docs/` directory** (`output-dir: docs` in `_quarto.yml`, repo name `HalfSpacePrince.github.io`). This means:

- The rendered `docs/` output **is committed to git** — it is the deployed artifact, not a build-time-only folder. After changing content, run `quarto render` and commit the regenerated `docs/` alongside the source.
- `_site/` and `.quarto/` are gitignored scratch/cache dirs and are NOT the deployment target — do not confuse them with `docs/`.

## Rules

- **Always `quarto render` before committing.** The live site serves from `docs/`; committing source changes without re-rendering leaves `docs/` stale and the deployed site out of sync.
- **The standard deploy sequence is: `quarto render` → `git add -A` → `git commit` → `git push origin main`.** When asked to deploy/ship/publish, run all four steps without asking for each separately.
- **Never run `rm` commands.**
- **Data files never live in this repo.** They live on the Seagate drive at `/Volumes/Seagate/Sharp Focus Advisory/`. Large binaries (PDFs, video decks) are linked out (e.g. Google Drive) rather than committed.

## Structure & conventions

- `_quarto.yml` — Site config: navbar, theme (`cosmo`), and the site-wide `execute: freeze: auto` setting.
- Top-level pages: `index.qmd` (landing/about-card via the `about:` front-matter template), `about.qmd`.
- **Sections and posts follow one pattern:** a *section* is a folder whose `index.qmd` is a grid **listing page** (e.g. `tactical-analysis/`, `recruitment/`); a *post* is a subfolder inside a section with its own `index.qmd`. The listing auto-indexes each post's `index.qmd` by its front-matter `date`/`title`/`description`/`image`, newest first — add a post by creating a new subfolder with that front matter and it appears automatically.
  - Each post subfolder keeps its own `images/`.

Some `index.qmd` links reference assets that may not exist yet (e.g. `cv.pdf`, `football-analytics.qmd`) — these are intentional placeholders, not broken references to fix unless asked.
