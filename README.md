# coates-media-shared-context

Single source of truth for content consumed by multiple Coates Media surfaces.

## What lives here

- `brand.md` — Coates Media brand reference (voice, colors, fonts, logo, etc.)
- `business-structure.md` — entities, infrastructure ownership, legal posture
- `working-style.md` — how Lexi expects agents and humans to communicate
- `coates-media-schema.md` — the Coates Media agency-level schema (clients, projects, ops)
- `meta-app/` — Meta App Submission docs (privacy policy, ToS, data deletion, app review checklist). These render as live pages on `coatesmedia.co` and as the Meta App's required URLs.

## Consumers (downstream repos that submodule this)

| Consumer | Mount path in consumer | Used for |
|---|---|---|
| `coates-media-ops` | `global-context/` | AI agent context, decision-making, registries |
| `coatesmedia-web` | `shared-context/` | Astro build inputs — renders brand info + (Sprint 2) live legal pages on `coatesmedia.co` |

## Update workflow

1. Edit a file in this repo
2. Commit + push to `main`
3. In each consumer repo: `git submodule update --remote <path>` to bump the submodule pointer, then commit + push
4. Cloudflare Pages (for `coatesmedia-web`) and `coates-media-ops` consumers pick up the change

The `platform-architect` agent owns this propagation workflow. See `coates-media-ops/agents/platform-architect/playbooks/shared-context-sync.md`.

## Why this repo exists

Before this, brand/legal content was duplicated:
- `~/Documents/Business/Coates Media/Claude/AIContext/brand.md` (local agent context)
- `coatesmedia-web/AIContext/brand.md` (Astro build input)
- `~/Documents/Business/Coates Media/Claude/MetaApp_Submission/privacy_policy.md` (local stash)
- `coatesmedia-web/MetaApp_Submission/privacy_policy.md` (Astro build input, deployed)
- `Zoho One - FADS/Sprint2_AttributionFix/MetaApp_Submission/privacy_policy.md` (FADS-Sprint2 draft)

Drift was inevitable. Now there's one source. The legacy local mirrors get archived during the `coates-media-ops` monorepo migration.

## What does NOT belong here

- Anything client-specific (FADS brand voice, FADS Zoho schema, FADS attribution logic) — that lives in `coates-media-ops/clients/<client>/`
- Credentials, API tokens, secrets — never. **This repo is public** (load-bearing for Cloudflare Pages submodule clones in `coatesmedia-web`; see `coates-media-ops/agents/platform-architect/playbooks/shared-context-sync.md` for the full reasoning). Treat anything pushed here as world-readable.
- Agent-specific playbooks — those live in `coates-media-ops/agents/<agent>/`
- Infrastructure code — that lives in `coates-media-ops/common/`
