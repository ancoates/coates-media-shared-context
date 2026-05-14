# Coates Media — Business Structure

> Shared context. Lives in `coates-media-shared-context`, consumed by `coates-media-ops` (as `global-context/business-structure.md`) and any future surface that needs to know who Coates Media is, structurally.

## Entities

### Coates Media LLC
- **Founder / sole proprietor:** Alexis "Lexi" Coates (lexi@lexilutions.com / ancoates@coatesmedia.co)
- **Function:** Marketing agency / marketing-ops consulting
- **Active clients:** see `coates-media-ops/registries/clients.yaml`
- **Banking:** _(fill in: Mercury, etc.)_
- **Payment processing:** _(fill in: Stripe, etc.)_
- **Accounting:** _(fill in)_
- **Legal:** _(fill in)_

### Lexilutions (parent / personal brand)
- Lexi's personal domain. Email `lexi@lexilutions.com` is the canonical address.

### Thread Lightly
- Screen printing / merch business
- _(fill in: entity status, role in Coates Media portfolio)_

### AKquire
- Marketing + tech hybrid startup, co-built with _(fill in)_
- _(fill in: entity status, current state, role relative to Coates Media)_

## Infrastructure owned by Coates Media (shared across clients)

- **Domain:** `coatesmedia.co` (production marketing site; legacy PHP currently live, Astro rebuild at preview.coatesmedia.co)
- **Email infrastructure:** `hello@coatesmedia.co` (general), Lexi's `ancoates@coatesmedia.co` (founder)
- **n8n automation host:** `ops.coatesmedia.co` (self-hosted, Docker, Caddy reverse proxy) — runs workflows for all clients
- **Meta App:** `FADS Lead Sync` (App ID `963876983267406`) — Meta App owned by Coates Media, currently scoped to FADS but architecturally available to other Meta-using clients via additional ad accounts.
- **Cloudflare Pages:** hosts `preview.coatesmedia.co` from `github.com/ancoates/coatesmedia-web`
- **cPanel (legacy):** hosts current production `coatesmedia.co` (PHP)
- **GitHub:** `github.com/ancoates/*` — repos: `coatesmedia-web`, `coates-media-ops`, `coates-media-shared-context`

## Banking & financial infrastructure
_(fill in. Pointer references only — never put actual account numbers in any repo. Use 1Password / Bitwarden / similar.)_

## Legal / compliance posture
- **Privacy policy:** master policy at `coatesmedia.co/privacy`, source in this repo at `meta-app/privacy_policy.md`
- **Terms of service:** at `coatesmedia.co/terms`, source at `meta-app/terms_of_service.md`
- **Data deletion:** at `coatesmedia.co/data-deletion`, source at `meta-app/data_deletion_instructions.md`
- _(fill in: contracts/SOWs convention, NDA handling, etc.)_

## Notes for AI agents reading this
- Treat this file as canonical for "who is Coates Media." If a client needs to know Coates Media's structure, this is the source.
- Anything marked `_(fill in)_` is a known gap. Don't fabricate. Either ask Lexi or surface the gap as a TODO.
