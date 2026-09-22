# Blevins Legislative Drafting

Companion to [`blevins-docket-mgr`](https://github.com/policynerd/blevins-docket-mgr).

This repository is the **newbuild** drafting suite: Akoma Ntoso instruments,
structured multi-document proposals, and Chromium-backed PDF export. It is
**not** the docket, calendar, votes, minutes, budget, or procurement system.

Those records stay in `blevins-docket-mgr` (`legacy/`). Drafting runs
alongside that system — Fly app `blevins-drafting` — and must never be
deployed over `beg-docket-manager`.

## What lives here

The source tree is copied from the docket monorepo's `apps/`, `packages/`,
`scripts/`, `Dockerfile`, and `fly.toml`.

| Path | Role |
| --- | --- |
| `apps/web` | Next.js drafting desk (proposals, documents) |
| `apps/api` | Fastify API, Entra sign-in, sessions |
| `packages/akn` | Akoma Ntoso parse / edit / serialize |
| `packages/db` | PostgreSQL schema and migrations |
| `packages/pdf` | Browser-grade PDF render + merge |
| `scripts/` | Container start and release |
| `fly.toml` | Fly app `blevins-drafting` only |

## Requirements

- Node.js ≥ 22.5
- pnpm (see `packageManager` in `package.json`)
- PostgreSQL 16
- Chromium (`pnpm exec playwright install chromium`)

## Run

```bash
pnpm install
export DATABASE_URL=postgres://localhost:5432/blevins
pnpm db:migrate
pnpm dev
```

## Relationship to the docket

The docket manager publishes agendas, takes rolls, and keeps the fiscal
record. This suite authors the instrument that later becomes a legislative
file on that docket. Do not collapse the two apps onto one Fly machine.
