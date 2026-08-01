# ReClaim API — Module A Test Suite (Bruno)

The same automated tests used for assessment — run them throughout the module.

## Setup (once)

1. Open Bruno → **Open Collection** → select this folder (choose **Developer Mode**
   if asked — the database reset step needs it)
2. Select the **Local** environment and fill in:
   - `baseUrl` — wherever your API runs
   - `dbName`, `dbUser`, `dbPass` (and `dbHost` / `dbPort` if not defaults) — your
     MySQL connection, so the suite can reset your data for you
   - the database may be local or remote — the suite connects directly with a
     bundled driver; nothing needs to be installed

## Testing one part at a time (recommended)

Right-click a folder → **Run**, in this order:

1. `A - reset` — re-imports `../database/reclaim-db.sql` into your MySQL database
   (needs none of your code; some tests change data, so always start here)
2. `A1 - auth` — stores the tokens the other folders use
3. The folder you are working on

## Running everything

Run from the collection root — folders execute in order, the database is reset at
the start and end automatically, and the run is repeatable.

The marking scheme and the tests are 1:1 — every measured row is one test line with the same id (`A1.1:` … `A9.3:`), wording, and order.
