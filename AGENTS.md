# Punta Agent Guide

**Human developers:** start with [README.md](README.md) and [docs/IMPLEMENTATION_PLAN.md](docs/IMPLEMENTATION_PLAN.md).

Org-wide agent defaults: see [room-tba/AGENTS.md](https://github.com/uplbtools/room-tba/blob/main/AGENTS.md). This file tailors that playbook to **punta** (planning phase).

## Status

**Planning repo: no `apps/*` packages yet.** Do not invent production code paths that contradict `docs/IMPLEMENTATION_PLAN.md`. Read the plan before scaffolding.

## Doc map

| When | Read |
| --- | --- |
| Product scope, milestones | [docs/IMPLEMENTATION_PLAN.md](docs/IMPLEMENTATION_PLAN.md) |
| Org roles / permissions model | [docs/ORG_ROLES.md](docs/ORG_ROLES.md) |
| Room TBA venue links | [room-tba](https://github.com/uplbtools/room-tba) map URLs / API (when integrated) |

## Planned stack (target: not all implemented)

- **Monorepo:** npm workspaces (`apps/*`, `packages/*`)
- **Web app:** Astro 7 + Svelte islands (per implementation plan)
- **Data:** Supabase Postgres + Drizzle
- **Auth:** Supabase Auth, org/event roles
- **Edge redirects:** Cloudflare Worker or Vercel edge for short links + click analytics
- **Media:** Cloudflare R2 for event assets
- **Deploy:** Vercel (SSR app) + edge workers

Align new code with **Room TBA** patterns where stacks overlap (Astro, Drizzle, Vercel env guards).

## Branches and deploy

- **Default branch:** `main` only (no `staging` until first app ships)
- Feature work: branch → PR to `main`
- When apps land, adopt **`staging` → `main`** like room-tba before production traffic

## Verify before done (when code exists)

| Step | When |
| --- | --- |
| `npm run lint` / `npm test` | Once real packages replace stub scripts |
| `bun run build` or app-specific build | Per app README |
| Migrations | Apply Supabase SQL before deploy when Drizzle lands |

Today stub scripts only echo: verification is **doc + plan consistency**.

## Domain rules (from plan)

- Short links and event pages are **org-scoped**: respect role matrix in `ORG_ROLES.md`
- Campaign analytics: click → registration → check-in: preserve audit trail; no PII in public logs
- Deep links to Room TBA venues should use stable slugs, not raw IDs in user-facing URLs

## How to work

- **Bias toward action** on scoped scaffolding: but **do not** build full product ahead of the plan
- **Preserve the dirty tree**; keep scope tight
- **`gh` by default** for issues and PRs
- Update `IMPLEMENTATION_PLAN.md` when milestones or stack choices change

## Commits

- Conventional Commits: `docs(plan): …`, `chore(monorepo): …`, later `feat(web): …`
- When creating issues, use size/priority labels if enabled on the repo
