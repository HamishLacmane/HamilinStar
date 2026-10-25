# PROJECT_LOG — HamilinStar

**Append-only.** Add new entries at the bottom; never edit or delete past lines (if something turns out wrong, add a new line saying so). Record key changes, decisions, gotchas, and things Hamish asked for. Format: `- YYYY-MM-DD — [change|request|decision|bug|todo] text`.

`CLAUDE.md` explains how the site works; this file records *what happened and when*. Data refreshes come from `../hamilin-star-db` (see its own log for the batch detail).

_Entries up to 2026-10-10 were backfilled from memory notes and CLAUDE.md history — dates are the ones recorded there._

## Log

- 2026-08-11 — [change] Site now reads `data/restaurants.json` (exported from Postgres); static, no backend.
- 2026-08-13 — [change] ⭐ favicon, SEO pass, tier-definition legend. `.star-nostar` made transparent/hairline instead of dusty pink.
- 2026-08-14 — [request] Default sort locked to "Most gold" (it kept drifting). Added a "Guide" column showing Hamilin Guide categories with Guide's colours.
- 2026-08-19 — [request] Tier legend redesigned to match Guide's category-def pattern (colour pill + plain text) and "Buy me a gelato" link added above the legend. Fixed a `.star-intro p` specificity bug along the way.
- 2026-08-27 — [request] Support link switched from PayPal.me to buymeacoffee.com/hamilingui6.
- 2026-08-30 — [request] Country/City/Cuisine/Food status/Guide category filters made multi-select (custom widget). Dining filter hidden. Guide-category filter now lists all 6 categories.
- 2026-08-30 — [request] Gmaps link: tried a map-pin-share icon under the name, moved to before the country text; dedicated GMaps column hidden. Sort `<select>` given the same chevron as the new buttons.
- 2026-09-19 — [change] Data re-export for the 2–19 Sep visits batch.
- 2026-10-01 — [change] Data re-export for the 23–30 Sep visits batch.
- 2026-10-10 — [request] Hamish asked for an append-only PROJECT_LOG.md per repo. Created this file.
- 2026-10-10 — [bug] Four commits (2026-09-19 and 2026-10-01 data-refresh PRs, both repos) carried a `Co-Authored-By: Claude` trailer, against Hamish's standing no-trailer rule for Hamilin repos (a harness attribution reminder arrived and should have yielded to that rule). Already merged; history not rewritten. No trailer on Hamilin commits going forward.
- 2026-10-11 — [change] Data re-export for the October visits batch (3/7/9 Oct): Suraj Sweet Mart, Nando's Cabot Place, new restaurant Pane Cunzato (restaurants 549 -> 550). Not yet committed.
- 2026-10-11 — [request] Hamish asked for the agents to be stored in git with their projects. Added `.claude/agents/hamilin-import-agent.md`, `.claude/agents/hamilin-export-agent.md` and `AGENTS.md` (identical copies in HamilinStar and HamilinGuide). Not yet committed.
- 2026-10-25 — [change] Import agent prompt updated (usual-orders shorthand); copy kept identical with the other repo and the working copy. Not yet committed.
- 2026-10-25 — [change] Agent prompts + AGENTS.md updated: temp files only inside the current project folder (Hamish's rule). Copies kept identical. Not yet committed.
- 2026-10-25 — [change] Re-exported data/restaurants.json (551 records, adds Punjab Restaurant) and data/stars.json (835 awards, was 826) after the 14-24 Oct 2026 visits batch. Not yet committed.
