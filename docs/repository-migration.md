# Repository migration — 04/11/2026

## Source and destination

- Source repository: [nguyenhonggiang2407/DTDD](https://github.com/nguyenhonggiang2407/DTDD).
- Source branch: [`yangdata`](https://github.com/nguyenhonggiang2407/DTDD/tree/yangdata).
- Source commit: [`587b812b5f74e5501e5acbcf45d17c10811d2389`](https://github.com/nguyenhonggiang2407/DTDD/commit/587b812b5f74e5501e5acbcf45d17c10811d2389).
- Source tree: `9373ff46a668c5a73eb176bc2a118616a4bffc1c`; nine reachable commits before migration.
- Destination: [nguyenhonggiang2407/YangData](https://github.com/nguyenhonggiang2407/YangData), branch `main`.

The extraction used `git clone --single-branch --branch yangdata`, with complete
reachable history rather than a shallow clone. The local branch was renamed to
`main`, and the source remote to `upstream`. No source branch, commit, data or
repository was deleted or rewritten. Publishing uses an ordinary push to the new
repository; the original DTDD branch remains available.

## Preservation and migration changes

The source commit remains an ancestor. Its original commit objects, authors,
dates and messages are retained. Before committing migration work, `git diff`
confirmed no change in `lib/`, `public/`, `test/`, `server.mjs`, dependency manifests,
Dockerfile, Compose, LICENSE, NOTICE or `upstream/`.

The MIT license blob remains `84ee68d33c9b68bae6c139f591996f021a02b23a` and NOTICE
remains `9d6b7aaf839f30b3cdcca827d24cdf5ea37172c1`. The original patchy631 attribution,
reference snapshot and preserved SQL-tool reference are unchanged. Read [NOTICE](../NOTICE.md)
for the distinction between reference material and YangData implementation.

Migration changes are limited to README clone/current-repository and CI links,
workflow branch filters targeting `main`, this record and screenshots from browser
verification. Historical/source-proof links continue to point to their original
location. The README documents the same query grammar, database and limits.
The existing CI retains backend, browser, Docker health and screenshot checks.

History can be checked after publication:

```sh
git merge-base --is-ancestor 587b812b5f74e5501e5acbcf45d17c10811d2389 main
git cat-file -t 587b812b5f74e5501e5acbcf45d17c10811d2389
git diff 587b812b5f74e5501e5acbcf45d17c10811d2389 main -- lib public test server.mjs package.json package-lock.json LICENSE NOTICE.md upstream
```

The first command should return 0; the second should return `commit`; the final
command should show no business-source, dependency or attribution change from extraction.

## Validation evidence

- Baseline at the exact source SHA: 35 backend/domain/store/HTTP tests passed on
  Node.js 24.19.0 during the 03/11/2026 audit. They are not rerun here merely for
  documentation changes; the new repository CI is configured to run them again.
- In the extracted repository on 04/11/2026, `npm ci` succeeded and reported zero
  dependency advisories at installation time.
- `npm run test:ui` passed all six Chromium tests against the real local server and
  in-memory SQLite: filter/grouped SQL/saved report/export; CSV types and safe rendering;
  invalid CSV/UTF-8; late responses; pagination and cascade; mobile workflow at 390 px.
- The test regenerated `desktop.png`, `mobile.png`, `query-plan.png` and `reports.png`
  in `docs/screenshots/`. These are captures of the running app with fictional sample
  data; desktop and mobile layouts were visually inspected. No screenshot or query
  output was synthesized.
- `git diff --check`, changed-file formatting and source/history preservation checks
  were performed before the migration commit.

Docker is not available through PATH or the checked Docker Desktop/Rancher Desktop
locations in this session, so no local Docker build/run is claimed. The new GitHub
Actions run and Docker smoke test must be inspected after the destination is published;
they had not run in that repository when this migration record was prepared.

There is no verified public deployment for YangData. It remains a private workspace
with the same cookie expiry, approximate SQLite REAL numbers, query quotas and
single-process limits documented in the README. Migration does not add billing or hosting.
