# Hamilin Star

Hamilin's food-rating system — part of the Hamilin brand family. Currently a placeholder shell, but the actual data now exists.

## Status

- **Data source — decided.** A standalone local Postgres database (`hamilin-star-db`, a sibling folder, not part of this repo) is the source of truth, refreshed periodically from Airtable. See that folder's `CLAUDE.md` for the full pipeline.
- **`data/restaurants.json`** — a flattened export of that database: one object per restaurant, star counts already computed (no client-side joins needed). Regenerate it via `hamilin-star-db/export.sql` whenever the underlying data changes, then copy the output here. Not yet wired into the page itself — `index.html` doesn't read this file yet.
- **Colours** — still not chosen. `styles.css` uses a neutral grey placeholder, not a real palette pick.

What exists now is a "coming soon" page plus the real data sitting alongside it — no framework, no build step, deploys to GitHub Pages with zero configuration.

## Licence

© 2026 Hamish Lacmane. All rights reserved. This code is provided for reference only and may not be copied, reused, or redistributed without permission.
