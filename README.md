# Artificially Greasy: vehicle specs pages

The owner's-manual specs pages at `https://artificiallygreasy.com/specs/`: one
page per vehicle-year (`/specs/<make>/<model>/<year>/`), the picker that links
to them all, the garage picker's vehicle list and the specs sitemap.

Everything under `public/` is **generated**. Nobody edits it by hand. It is
written by `scripts/build_specs.py` in the main repository
([Semi-Synthetic-Intelligence](https://github.com/nathanpool96-ai/Semi-Synthetic-Intelligence)),
which is where the templates, the rules and the tests live.

## How it deploys

This repository has its own Cloudflare Worker, `artificially-greasy-specs`,
connected with Workers Builds: a push deploys. There is no build step; the
deploy command uploads `public/` as static assets (`wrangler.jsonc`). The
Worker answers only on `artificiallygreasy.com/specs*`. Every other path on
the site is the main repository's Worker.

The pages load the main site's stylesheets and scripts and link to its job
pages by root-absolute paths (`/styles.css`, `/garage.js`, `/job/...`), which
work because both Workers share the hostname.

## What's in `public/`

| Path | What |
|---|---|
| `specs/index.html` | the picker, `/specs/` |
| `specs/<make>/<model>/<year>/index.html` | one specs page per vehicle-year |
| `specs/index.json` | the vehicle list the garage picker reads |
| `specs/sitemap.xml` | the picker and every indexable page (the main `sitemap.xml` index lists it) |
| `_headers` | keeps `specs/index.json` out of search results |

## Regenerating

Only when the knowledge release, its audit, the hold list or the templates
change. From the main repository:

1. `knowledge release`, then `knowledge audit` (see the main repository's
   `CLAUDE.md` for the environment they need). Point `specs-build.json` at the
   new release and audit.
2. `python scripts/build_specs.py --out <this repository>/public`
3. Review the diff here. Every page is rewritten, but unchanged pages come out
   byte-identical, so the diff shows only real changes.
4. Commit and push. The push is the deploy.

The manuals, the knowledge store and the releases stay on the machine that
generates, never in git.
