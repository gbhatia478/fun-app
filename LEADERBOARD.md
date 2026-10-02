# Shared high scores

The game remains at https://gbhatia478.github.io/fun-app/ with no frontend build step.
The leaderboard API is https://samit-high-scores.gbhatia.chatgpt.site, hosted with Sites and backed by Cloudflare D1.

Sites project: `appgprj_6abf035961d081918cc9b01d29d298ea`. Database binding: `DB`.

The service source lives in `leaderboard-service/`, which is a separate, managed Git repository. The outer GitHub repository ignores this directory so it cannot accidentally become a submodule. Sites retains the service source and its migrations; reuse this existing project when updating or restoring it.

## Behavior

- Show the three highest scores, with earlier entries winning ties.
- Ask for 1–3 letter initials after a qualifying run ends.
- Store initials in uppercase. No name, account, or email is required from players.
- Recheck qualification when saving so simultaneous players cannot displace a better score incorrectly.
- Retrying a save cannot create duplicate entries for the same run.
- If the service is unavailable, the game still works; a failed initials save preserves the form for retry.

The database contains `runs` (server-issued run ID, start time, final score, finish time) and `scores` (run ID, initials, score, creation time). The leaderboard is public, matching the existing game's audience. Browser requests are allowed from the game's GitHub Pages origin.

The server rejects malformed entries and scores exceeding elapsed time plus a short network grace period. This is a casual leaderboard; the server does not replay and verify every jump.

## Service development

Run `npm test` inside `leaderboard-service/` to check persistence, ordering, ties, save retries, qualification races, and input validation. These tests use a separate local SQLite database and do not add live scores.

For schema changes, update `db/schema.ts`, run `npm run db:generate`, and review the new migration. Preserve already-deployed migrations. Use the Sites hosting skill's managed source workflow to test, build, push, package, and deploy the same Sites project. Keep deployment credentials in memory and stdin, never in source files or shell arguments.

The service's build copies its dependency-free Worker into `dist/server/index.js`. The Sites packager includes the Drizzle migrations and provisions the production D1 database. The browser contains only the public API URL; it has no database credentials.
