# Production deployment

The infrastructure authority is `/Users/suenot/projects/server/docs/harness-analyzer.md`;
service locations and access are listed in `/Users/suenot/projects/server/SERVICES.md`.
Use those documents for credentials and deployment procedures.

The frontend deploys automatically on a push to `frontend/main` through the
Vercel project `harness-analyzer`. The API and PostgreSQL run in
`/home/suenot/harness-analyzer` on Server 1. API deployment synchronizes sources
without `.git`, `node_modules`, `dist`, `.env`, `data`, `backups` or `reference`,
then runs the documented Compose config, build and startup commands. Before
schema changes, copy the session cache and create a PostgreSQL custom-format
backup; verify its restore listing and SHA-256 checksums.

## 0.5.0 — 2026-10-02

- Root release: `b56c275`; API: `b187e5a` (backend 0.4.0); frontend:
  `29a42b6` (frontend 0.5.0). All changes were pushed to their `main` branches.
- Verified backup on Server 1:
  `/home/suenot/harness-analyzer/backups/selected-sharing-20261001T210113Z`.
  It contains the database dump, session cache, restore listing, checksums and
  baseline row counts. The previous API image was retained for rollback.
- The API was rebuilt and restarted with `docker-compose.prod.yml`; the new
  image is `sha256:f1d7f4792aa4888065160ce64440eb9785d01a9d0c1365e920e8b37c2c21fb81`.
  The migration added `audience`, `allowed_emails` and `allowed_group_ids`,
  preserving existing visibility settings. Profile/snapshot/device snapshot
  counts remained 2/1/2.
- [Vercel deployment](https://vercel.com/suenots-projects/harness-analyzer/5fbr5LPj1ZPgCbDgGJoWD3fwQMjn)
  completed successfully. The production JS bundle includes the audience
  picker, email recipients and authenticated group loader.
- Validation: 71 backend tests, 17 relevant frontend tests, frontend build,
  and real PostgreSQL checks for migration idempotency, legacy defaults,
  selected recipients, shared analytics gates and leaderboard exclusion.
- Production smoke checks: readiness and leaderboard return 200; `/profile`
  and `/users` load successfully; owner settings, groups and private analytics
  require authentication; unavailable shared pages return uncached 404 even
  with an invalid JWT; existing private and missing profiles return identical
  404 responses on dashboard, Sessions and Projects.

Selected group grants use current viewer membership on each group-based read.
A newly selected group must belong to the profile owner. Saved grants stay in
place until removed in Profile, including if the owner later leaves a group.
A deleted group grants no access. The UI allows removing saved groups that
are no longer in the owner's current list.
