# Market briefing publishing

- `/` is the US market briefing. It uses the same absolute `/us-market-briefing/reports.json` and `/us-market-briefing/regime-reports.json` paths as the original briefing URL.
- `/crypto-market-briefing/` is the native GitHub Pages crypto briefing and narrative report. It reads only same-origin JSON; no private Site tokens are shipped to visitors.
- `/blog/` preserves the original GitBook home, with its existing lecture/post menus. `README.md` owns that permalink.
- Shared navigation is `assets/market-navigation.js`. Preserve this include during any HTML update.

After each successful crypto Site publication, the linked 07:30 KST cloud task must read back both complete lists from the owned Site using supported service access and mirror non-demo records to:

1. `crypto-market-briefing/data/reports.json`
2. `crypto-market-briefing/data/insights.json`
3. Date snapshots under `crypto-market-briefing/data/daily/YYYY-MM-DD.json` and `data/reports/YYYY-MM-DD.json`.

Use authenticated GitHub tools for repository `bestinvesting/bestinvesting.github.io`, branch `main`. Read the current ref and commit tree; build an additive tree over the current tree; commit all changed JSON together; update the ref with expected_sha and no force. On a concurrent change, fetch the new head, preserve unrelated edits, and retry the merge. Preserve every earlier date; do not replace a full list with only today's entry. Git commit history preserves same-day revisions.

Do not copy access tokens, private operational instructions, or user account information. Public market report content is authorized for this public blog. If either publication fails, state which destination succeeded and which failed. A GitHub commit is not proof that Pages deployment succeeded; check the deployment workflow status.

The US update task continues to update `us-market-briefing/reports.json` and regime records. The homepage reads those same files, so it updates together without duplicating data. Preserve the shared menu script and absolute data routes if refreshing briefing HTML.
