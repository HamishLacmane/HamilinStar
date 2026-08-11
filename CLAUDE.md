# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is (currently)

A live filterable restaurant browser (`index.html` + `styles.css`, no framework, no build step, deploys to GitHub Pages with zero configuration) reading `data/restaurants.json`. The old "coming soon" placeholder hero was explicitly replaced with this at Hamish's request (2026-08-11) — do not reintroduce a coming-soon shell, that decision is made.

- `index.html` fetches `data/restaurants.json` client-side and renders every restaurant as a row in a `<table>` (sticky dark header using the existing `--ink` token, zebra striping, hover highlight). Toolbar above it: search box, filters for country/city/cuisine/food status, and a sort dropdown (name/gold/total stars/review count). Columns: Name, Location, Cuisine, Food. **No Dining column** — removed 2026-08-11 because the underlying data is too sparse to be worth a column; the dining-option filter dropdown still works, it's just not displayed per-row.
- Star badges (gold/silver/bronze/no-star/pending) use fairly saturated medal colours (`.star-gold`, `.star-silver`, etc. in `styles.css`) — these are informational/functional, not a brand palette decision, so they're fine to keep even though Star's real colours are still undecided (see below).
- **Planned, not built:** a second page showing per-dish current tier (not the raw Hamlin Stars award-level table), with the star badges on the main table linking to it via a URL query param (e.g. `stars.html?restaurant=X`) so it's shareable/bookmarkable. Explicitly deferred by Hamish 2026-08-11 — don't build until asked.

## Data source — decided, lives outside this repo

`hamilin-star-db` (a sibling folder, `C:\Users\Hamish\Documents\Claude_code\hamilin-star-db\`) is a standalone local Postgres database — the source of truth for ratings data, refreshed periodically from Airtable. Full pipeline/schema/rationale documented in that folder's own `CLAUDE.md`. This repo does **not** talk to Postgres directly (it's a static GitHub Pages site, no backend) — instead:

- `data/restaurants.json` here is a **flattened, pre-computed export** — one object per restaurant, star counts (gold/silver/bronze/total for food/service/hygiene) already calculated, cuisine tags and dining options as plain arrays. No client-side joins needed; `fetch()` + `Array.filter()`/`.sort()` is enough, and that's exactly what `index.html` does.
- Generated via `hamilin-star-db/export.sql` (run through `psql`, output piped to a file), then copied into this repo by hand. **Not automated** — regenerate and re-copy whenever the underlying data changes. Every data correction this session (Airtable edit → Postgres rebuild → re-export → copy → verify) followed this exact manual loop.

Do not invent a different data source, wire up a live database connection, or build against anything other than this JSON file — the static-export approach was deliberately chosen because this is a plain GitHub Pages site with no server.

## Colours are not decided

`styles.css` uses a neutral grey (`--accent: #8A8A8A`) as an explicit placeholder, not a real brand choice. Don't treat it as the final palette or extend it as if it were — Hamish hasn't picked Star's colours yet. The table's dark sticky header reuses the existing `--ink` token (not a new colour), and the star-tier badge colours are conventional medal colours (informational, not brand) — both are fine to keep despite the palette still being undecided; don't read either as a resolved brand choice.

## Verification workflow — don't ship UI changes unverified

Before pushing any `index.html`/`styles.css` change, serve the repo locally (`python -m http.server <port>` from the repo root) and check it in the Browser tool — `read_console_messages` for JS errors, `javascript_tool` to inspect actual rendered DOM/computed styles (row counts, filter results, computed colours), not just eyeballing. Screenshot capture has been unreliable in this environment; DOM/JS inspection has been the reliable fallback all session. After pushing, re-check the **live** site too — Cloudflare's edge cache has shown transient stale responses on the first request after a deploy that clear up on retry, so don't treat one stale-looking fetch as a real bug without retrying.

## Licence

No LICENSE file by design — all rights reserved by default. Don't add an open-source license without being explicitly asked to change that.

## Git workflow

`gh` CLI is not installed on this machine — PRs can't be created programmatically. Push the feature branch and hand Hamish the GitHub "create PR" URL GitHub prints on push (`github.com/HamishLacmane/HamilinStar/pull/new/<branch>`). After Hamish merges, **check whether the branch still exists on origin before reusing it** — he periodically deletes merged branches via the GitHub UI, so a local branch that still has commits queued may need a fresh branch cut from `main` rather than assuming the old remote branch is still there.
