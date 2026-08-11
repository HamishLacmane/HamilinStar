# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is (currently)

A placeholder "coming soon" page (`index.html` + `styles.css`, no framework, no build step, deploys to GitHub Pages with zero configuration) — plus a real data export (`data/restaurants.json`) that the page doesn't consume yet.

## Data source — decided, lives outside this repo

`hamilin-star-db` (a sibling folder, `C:\Users\Hamish\Documents\Claude_code\hamilin-star-db\`) is a standalone local Postgres database — the source of truth for ratings data, refreshed periodically from Airtable. Full pipeline/schema/rationale documented in that folder's own `CLAUDE.md`. This repo does **not** talk to Postgres directly (it's a static GitHub Pages site, no backend) — instead:

- `data/restaurants.json` here is a **flattened, pre-computed export** — one object per restaurant, star counts (gold/silver/bronze/total for food/service/hygiene) already calculated, cuisine tags and dining options as plain arrays. No client-side joins needed; `fetch()` + `Array.filter()`/`.sort()` is enough.
- Generated via `hamilin-star-db/export.sql` (run through `psql`, output piped to a file), then copied into this repo by hand. **Not automated** — regenerate and re-copy whenever the underlying data changes.
- `index.html` does not fetch or render this file yet — the actual filterable UI hasn't been built. Don't assume it's wired up just because the data file exists.

Do not invent a different data source, wire up a live database connection, or build against anything other than this JSON file — the static-export approach was deliberately chosen because this is a plain GitHub Pages site with no server.

## Colours are not decided

`styles.css` uses a neutral grey (`--accent: #8A8A8A`) as an explicit placeholder, not a real brand choice. Don't treat it as the final palette or extend it as if it were — Hamish hasn't picked Star's colours yet.

## Content is placeholder — do not write copy

The headline and intro paragraph are literal placeholder text / `TODO(Hamish)` comments. Hamish writes his own site copy; don't fill these in.

## Licence

No LICENSE file by design — all rights reserved by default. Don't add an open-source license without being explicitly asked to change that.
