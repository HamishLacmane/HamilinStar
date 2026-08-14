# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is (currently)

A live filterable restaurant browser (`index.html` + `styles.css`, no framework, no build step, deploys to GitHub Pages with zero configuration) reading `data/restaurants.json`. The old "coming soon" placeholder hero was explicitly replaced with this at Hamish's request (2026-08-11) — do not reintroduce a coming-soon shell, that decision is made.

- `index.html` fetches `data/restaurants.json` client-side and renders every restaurant as a row in a `<table>` (sticky dark header using the existing `--ink` token, zebra striping, hover highlight). Toolbar above it: search box, filters for country/city/cuisine/food status, and a sort dropdown (name/gold/total stars/review count). **Default sort is "Most gold" (`<option value="gold" selected>`) — locked in 2026-08-14, do not change without being asked again.** (History: was Name A–Z, changed to "Most total stars" 2026-08-12, then to "Most gold" 2026-08-14 after Hamish noticed the default kept drifting between commits — if this needs touching again, this is the *only* line to change: the `selected` attribute on `#f-sort`'s `<option>` elements in `index.html`. Don't let an unrelated edit silently move it.) Columns: Name, Country, City, Location name, Cuisine, Food, GMaps (GMaps column added 2026-08-13, links restaurant's Gmaps URL, "GMaps ↗" text, opens new tab). **No Dining column** — removed 2026-08-11 because the underlying data is too sparse to be worth a column; the dining-option filter dropdown still works, it's just not displayed per-row. Restaurant name in the Name column now links to `stars.html?restaurant=X` (added 2026-08-13), same as the star badges already did. **"Guide" column added 2026-08-14** to both `index.html` and `stars.html` — shows the restaurant's Hamilin Guide categories (if any) as colored pill badges, reusing Guide's own `--cat-*` colour tokens (now duplicated into this repo's `styles.css` too, values kept identical — see `hamilin-star-db`'s `export.sql`/`export_stars.sql` notes for where `guide_categories` comes from). `--cat-desserts` is a first-pass colour, not yet confirmed with Hamish.
- Star badges (gold/silver/bronze/no-star/pending) use fairly saturated medal colours (`.star-gold`, `.star-silver`, etc. in `styles.css`) — these are informational/functional, not a brand palette decision, so they're fine to keep even though Star's real colours are still undecided (see below). Badges link to `stars.html?restaurant=X` (built 2026-08-11 — see below, this used to say "planned, not built").
- **`stars.html`** — a second page, filterable table of every individual food/service/hygiene award (Restaurant, Country, City, Location name, Name, Category, Tier, Date Awarded, plus a Justification tooltip on the Tier badge when a record has one), reading a companion export `data/stars.json` (from `hamilin-star-db/export_stars.sql`). Service/Hygiene are currently hidden site-wide (both this page and index.html's per-row tags) behind a `SHOW_NON_FOOD = false` constant in each file's script — data isn't deleted, just filtered at render time; flip both flags back to `true` together once service/hygiene data is more complete. **`SHOW_NON_FOOD`'s filter only excludes `category === 'Service'` and `category === 'Hygiene'`, not everything except `'Food'`** — a `Shake` category was added 2026-08-12 (milkshakes, split out from generic `Food`) and must stay visible alongside Food when non-food categories are hidden; don't revert this to a `=== 'Food'` allowlist, it would silently hide every Shake award again. Both pages share a top-level `.section-nav` (Restaurants / All Stars Awarded tab pair) right below the topbar.

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
