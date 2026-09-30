# CLAUDE.md: the specs repository

- **Generated output only.** Everything under `public/` is written by
  `scripts/build_specs.py` in the main repository,
  `C:\Users\natha\OneDrive\Documents\ArtificiallyGreasey\ArtificiallyGreasy`
  (GitHub `nathanpool96-ai/Semi-Synthetic-Intelligence`). Never hand-edit it;
  change the generator or its templates there, then regenerate.
- **The main repository's `CLAUDE.md` applies here.** A session started in this
  directory does not load it; read it first. Its non-negotiables (never invent a
  torque value or part number, no model approves a fact, one commit per step,
  stop and report) hold for everything this repository ships.
- **Pushing deploys.** This repository is connected to the
  `artificially-greasy-specs` Worker with Workers Builds. Push only when Nathan
  says so.
- **Regenerate, review, commit, push** (README.md, "Regenerating"). Review the
  diff before committing: unchanged pages are byte-identical, so anything in the
  diff is a real change to a live page.
- **Never weaken the build's refusals** (a release without its audit, held
  vehicles, audit-flagged rows) to make a regeneration go through.
- **OneDrive** marks the folders it syncs read-only; `build_specs.py` clears the
  flag when it empties `public/specs/`.
