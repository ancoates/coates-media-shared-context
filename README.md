# coates-media-shared-context

Single source of truth for content consumed by multiple Coates Media surfaces.

## What lives here

- `brand.md` — Coates Media brand reference (voice, colors, fonts, logo, etc.)
- `business-structure.md` — entities, infrastructure ownership, legal posture
- `working-style.md` — how Lexi expects agents and humans to communicate
- `coates-media-schema.md` — the Coates Media agency-level schema (clients, projects, ops)

## Consumers (downstream repos that submodule this)

| Consumer | Mount path in consumer | Used for |
|---|---|---|
| `coates-media-ops` | `global-context/` | AI agent context, decision-making, registries |
| `coatesmedia-web` | `shared-context/` | Astro build inputs — `brand.md` + `coates-media-schema.md` (legal pages are owned natively by that repo, not sourced here) |

## Update workflow

1. Edit a file in this repo
2. Commit + push to `main`
3. In each consumer repo: `git submodule update --remote <path>` to bump the submodule pointer, then commit + push
4. Cloudflare Pages (for `coatesmedia-web`) and `coates-media-ops` consumers pick up the change

The `platform-architect` agent owns this propagation workflow. See `coates-media-ops/agents/platform-architect/playbooks/shared-context-sync.md`.

## Why this repo exists

Before this, brand content was duplicated:
- `~/Documents/Business/Coates Media/Claude/AIContext/brand.md` (local agent context)
- `coatesmedia-web/AIContext/brand.md` (Astro build input)

Drift was inevitable. Now there's one source. The legacy local mirrors get archived during the `coates-media-ops` monorepo migration.

> **Legal docs note (2026-06-04):** the Meta App legal docs (privacy policy, ToS,
> data-deletion instructions) used to live here under `meta-app/`. They were
> relocated into the `coatesmedia-web` repo (`src/content/legal/` + `legal/`)
> because the website was the only thing that rendered them — keeping them in a
> shared submodule only created copy-and-sync drift. The Meta App Review checklist
> moved to `coates-media-ops` (`clients/coates-media-internal/assets/meta-app/`).
> This repo now holds brand + schema + working-style only.

## What does NOT belong here

- Anything client-specific (FADS brand voice, FADS Zoho schema, FADS attribution logic) — that lives in `coates-media-ops/clients/<client>/`
- Credentials, API tokens, secrets — never. **This repo is public** (load-bearing for Cloudflare Pages submodule clones in `coatesmedia-web`; see `coates-media-ops/agents/platform-architect/playbooks/shared-context-sync.md` for the full reasoning). Treat anything pushed here as world-readable.
- Agent-specific playbooks — those live in `coates-media-ops/agents/<agent>/`
- Infrastructure code — that lives in `coates-media-ops/common/`
