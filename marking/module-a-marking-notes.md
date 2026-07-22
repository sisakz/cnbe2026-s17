# Module A — API "ReClaim" — Marking Instructions

## What you need

- Bruno
- The `api-tests` collection and the `database/reclaim-db.sql` dump
- The competitor's: API base URL, MySQL database name and credentials

## Marking a competitor

1. Open Bruno → **Open Collection** → the `api-tests` folder. If asked about the JavaScript sandbox, choose **Developer Mode** (the database reset scripts need it)
2. Select the **Competition** environment and set:
   - `baseUrl` — the competitor's API base URL
   - `dbName`, `dbUser`, `dbPass` (+ `dbHost` / `dbPort` if not local) — the competitor's MySQL database
   - `mysqlPath` — full path to the `mysql` client if it is not on PATH
3. **Run the collection from the root.** The first request re-imports the seed dump into the competitor's database (no competitor code involved), `A1 - auth` captures tokens, and the final request restores the database again. Runs are repeatable — re-run freely
4. Record results top to bottom: test names carry the sub-criterion prefix (`A1:` … `A8:`), in the same order as the marking scheme

## Awarding rules

- An aspect is awarded only when **all** of its tests pass — where one aspect covers several behaviours (a working endpoint and its 404, a rule and its 422), error handling is never awarded on its own
- **A9 exceptions — not covered by test results:**
  - *Passwords stored hashed* — inspect the database: `SELECT password FROM users LIMIT 1;` must show a hash (e.g. `$2y$...`), never plain text
  - *Base URL mounting* — awarded if the suite ran successfully at the competitor's deployed base URL (root or sub-path)
  - *Code quality (J)* — expert review of the submitted source; rubric 0-3 in the marking scheme

## Troubleshooting

- **`A - reset` red** — check the `db*` variables and `mysqlPath`; the import runs on the marking machine, not through the API
- **Everything 401 after A1** — the competitor's login is failing; mark A1 from what you see, later folders will largely fail as a consequence (that is a genuine result, not a tooling fault)
- **Partial re-check of one area** — run `A - reset`, then `A1 - auth`, then the folder in question
