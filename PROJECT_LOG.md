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
- 2026-11-01 — [change] Re-ran all three exports after the Nando's Cabot Place visits (28 and 29 Oct 2026, 4 reconfirmed dishes); restaurants.json 551, stars.json 835, guide.json 70 records, output byte-identical to the committed data (reconfirms changed no exported field). Not yet committed.
- 2026-11-08 — [change] Re-exported data/restaurants.json (552 records, adds Sambal Express) and data/stars.json (839 awards, was 835) after the 2-7 Nov 2026 visits batch (12 dish-visits; new dishes at The Veg Box Cafe and Sambal Express). Not yet committed.
- 2026-11-16 — [change] Re-exported restaurants.json (553; adds Shayona Restaurant, renames Shayone -> Shayona Sweets & Savouries, Veg Box Cafe now Still Cooking / top_picks) and stars.json (845; +6 Shayona Restaurant dishes, 2026-11-08). Not yet committed.
- 2026-11-19 — [change] Re-exported restaurants.json (554; adds Seoul90 Korean Restaurant, Nando's Cabot Place food gold 3 -> gold 2 / silver 1) and stars.json (850; +5 Seoul90 awards dated 2026-11-18, Nando's Cabot Place Sunset Burger Gold replaced by Silver 2026-11-18). Not yet committed.
- 2026-11-19 — [change] Re-exported restaurants.json (554, unchanged count; Seoul90 Korean Restaurant now Still Cooking with guide_categories amazing_value + top_picks) after giving Seoul90 Guide categories in Postgres; stars.json (850) unchanged. Not yet committed.
- 2026-11-19 — [change] Added snack exports: data/snacks.json now published (first 10 snacks, all UK) alongside restaurants/stars.
- 2026-11-19 — [change] Draft HamilinStar/snacks.html + Snacks nav tab (index.html, stars.html) + chip CSS appended to styles.css; reads data/snacks.json (10 sample snacks). Draft only, not committed.
- 2026-11-19 — [change] snacks.html draft: tier Definitions legend copied from index.html ('dish' -> 'snack'). Not committed.
- 2026-11-19 — [change] snacks.html draft: homepage intro + support link copied (restaurant -> snack), pack note shown under size. Not committed.
- 2026-11-19 — [change] Re-exported snacks.json from Postgres: 17 snacks (7 new undated multipacks), new pack_note field on every record; restaurants/stars/guide unchanged. Not committed.
- 2026-11-19 — [bug] Removed the 60ch max-width on .star-intro p (and .snack-note) in styles.css so the intro text fills the page width instead of wrapping at about half; snacks.html also now reads ?q= to pre-fill the search (used by the Guide's link). Not committed.
- 2026-11-19 — [change] Re-exported snacks.json: dietary tags added to 5 existing snacks (Walkers French Fries x3, Lindt Creation Hazelnut Wafer, McCoy's Salt & Malt Vinegar); no other data changed.
- 2026-11-19 — [change] AGENTS.md: added the 'Pre-push visual check' standing rule (all pages at phone/tablet/laptop/desktop sizes before any push) + CLAUDE.md pointer. Not committed.
- 2026-11-19 — [change] Re-exported all five JSON files from Postgres: snacks.json now derives Top Picks for every currently-Gold snack still made (7 snacks; Sainsbury's Bourbon also has Amazing Value); restaurants/stars unchanged. Not committed.
- 2026-11-19 — [change] snacks.html columns reordered to match the other Star pages, compact layout + inline Tier badge below 1100px. Not committed.
- 2026-11-19 — [change] Re-exported snacks.json: 'Most shops' is now exclusive (retailers shortened to ['Most shops'] on 8 snacks) and Silver still-made snacks tagged Worth a Try (17 snacks).
- 2026-11-21 — [change] Re-exported restaurants.json (555, +Pure, London, Canary Wharf - Cabot Square, Postgres-only) and stars.json (851, +Pure 'Hot Chocolate - Almond Milk', Drink, no star). Not committed.
- 2026-11-21 — [change] Re-exported restaurants.json (555) and stars.json (852) after Shayona Restaurant (Neasden) visit: new dish Chilli Paneer (No Star) and Pav Bhaji Bronze -> No Star; Shayona food counts now bronze 4, no_star 3. Not committed.
- 2026-11-21 — [change] Re-exported snacks.json (63 snacks, 46 new) after snack batch; restaurants.json and stars.json unchanged. Not committed.
- 2026-11-21 — [change] Pre-push visual check passed (all pages, 7 sizes, no overflow/console errors); committing + pushing on feature/snacks-and-nov-restaurant-update.
