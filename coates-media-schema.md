# Coates Media — Schema & Reference

**Purpose:** Single source of truth for system identifiers, accounts, infrastructure, conventions, and operational details for Coates Media LLC. Designed to be loaded as context for any AI agent (Claude, GPT, etc.) working on Coates Media's own business or any client work executed under it.

**Last updated:** 2026-05-10
**Maintained by:** Alexis "Lexi" Coates

---

## Table of Contents

1. [Business Details](#business-details)
2. [People & Operating Setup](#people--operating-setup)
3. [Domains & Hosting](#domains--hosting)
4. [Email Addresses](#email-addresses)
5. [Operational Tools](#operational-tools)
6. [Services Offered](#services-offered)
7. [Clients (Public)](#clients-public)
8. [Conventions](#conventions)
9. [Maintenance](#maintenance)

---

## Business Details

| Item | Value |
|---|---|
| Legal name | Coates Media LLC |
| Entity type | Limited Liability Company |
| State of formation | Texas |
| Year founded | 2022 |
| Headquarters | Lubbock, TX |
| Operator | Alexis "Lexi" Coates (sole operator) |
| EIN / tax info | [FILL: if relevant for AI work] |

---

## People & Operating Setup

Coates Media is a **sole-operator studio.** Lexi handles strategy, design, code, automation, CRM architecture, and client management herself. Collaborators may be brought in on a per-project basis but there is no full-time team.

| Person | Role |
|---|---|
| Alexis "Lexi" Coates | Founder, operator, everything |

---

## Domains & Hosting

All domains are registered through **GoDaddy** under Lexi's account.

| Domain | Use | Hosting | SSL |
|---|---|---|---|
| `coatesmedia.co` | Primary Coates Media domain (website, email, ops infrastructure) | (Currently WordPress; in process of migrating to Astro/Cloudflare or similar — see Coates Media Website project) | GoDaddy (expensive — considering Namecheap migration) |
| `threadlightlymerch.com` | Lexi's screen-printing / merch side business | cPanel under coatesmedia.co Web Hosting Deluxe (shared hosting account) | Namecheap |
| `lexilutions.com` | Owned but unused for web. **Used only for email** because most existing clients have her at this address from earlier work. | n/a | n/a |
| `sarahmichellehair.com` | Client website (Sarah Michelle Hair) | cPanel under coatesmedia.co Web Hosting Deluxe | Namecheap |

### Active subdomains under coatesmedia.co

| Subdomain | Purpose |
|---|---|
| `ops.coatesmedia.co` | Self-hosted automation infrastructure (n8n + Postgres on Hetzner) — see FADS automation stack docs |
| `coatesmedia.co/privacy` | Master privacy policy (referenced by Meta App Review) |
| `coatesmedia.co/terms` | Master terms of service |
| `coatesmedia.co/data-deletion` | Master data deletion entry point |
| `coatesmedia.co/<client-slug>-<app-slug>/data-deletion` | Per-app data deletion pages (e.g., `/fads-lead-sync/data-deletion`) |

**Hosting note:** there's a planned overhaul of `coatesmedia.co` from WordPress to a modern static-first stack (Astro/Cloudflare Pages or Vercel) — see the Coates Media Website project. The legal/policy URLs above are required to be live before Meta App Review can submit.

---

## Email Addresses

| Address | Use |
|---|---|
| **`ancoates@coatesmedia.co`** | **Primary customer-facing email** for Coates Media work. Self-hosted via cPanel server email. |
| `lexi@lexilutions.com` | Microsoft 365. Legacy email used by existing clients who have her at this address from earlier work. Active but secondary. |
| (ThreadLightly business email) | Microsoft 365 under threadlightlymerch.com. Personal/side-business use. |

Lexi runs solo, so role-based emails (hello@, support@, billing@) are not currently set up. Can be added if a specific use case requires it.

---

## Operational Tools

| Category | Tool | Notes |
|---|---|---|
| **Banking** | Mercury Banking | Primary business banking |
| **Payment processing** | Stripe | For client invoicing and any direct payments |
| **Accounting** | Zoho Books (standalone subscription, Coates Media-owned) | Bookkeeping, invoicing, financial reports. **Important:** this is a standalone Zoho Books subscription paid for by Coates Media — it is NOT part of any client's Zoho One. See "Client-owned tools" section below for the distinction. |
| **Email — Coates Media** | Self-hosted cPanel email at coatesmedia.co | Server-managed |
| **Email — Lexilutions / ThreadLightly** | Microsoft 365 | Legacy / side businesses |
| **Domains** | GoDaddy | All four domains |
| **Web hosting** | GoDaddy Web Hosting Deluxe (cPanel) | Hosts Sarah Michelle Hair + Thread Lightly + (currently) coatesmedia.co WordPress |
| **SSL — coatesmedia.co** | GoDaddy SSL | Expensive; considering Namecheap migration |
| **SSL — Sarah Michelle Hair, Thread Lightly** | Namecheap | |
| **Automation infrastructure** | Self-hosted n8n + Postgres on Hetzner Cloud at `ops.coatesmedia.co` | See FADS automation stack docs for architecture |
| **AI** | Claude Max plan (Claude Code, Claude.ai), Anthropic API for n8n workflow escalation | |
| **Code editors** | VS Code, Claude Code | |

---

## Client-owned tools (NOT for Coates Media use)

Some platforms Lexi works in extensively under client engagements are owned and paid for by those clients, not by Coates Media. They are explicitly **off-limits** for Coates Media's own operations — even though they're in active daily use during client work.

| Tool | Owned by | Notes |
|---|---|---|
| **Zoho One** (CRM, Mail, Campaigns, Analytics, Flow, Creator, Voice, Bookings, Desk, SalesIQ, etc.) | Fred Astaire Dance Studios (Philip Gutierrez Studio Group) | FADS pays the Zoho One license. Lexi operates within it for FADS work only. **Not** to be repurposed for Coates Media leads, email, automation, content, or any non-FADS use. Coates Media's own Zoho Books subscription (above) is a separate, standalone product. |

### Per-client schema convention

Each client may have their own CRM ecosystem, ad platforms, email infrastructure, and tooling — and those should be documented in **that client's own schema.md**, not in this Coates Media schema.md.

Going forward, every active client should have a dedicated schema file:

- `FADS_schema.md` — Fred Astaire Dance Studios stack (Zoho One, Meta Business, Google Ads, etc.)
- `OsteoStrong_schema.md` — OsteoStrong stack
- `Masakali_schema.md` — Masakali stack
- `SarahMichelleHair_schema.md` — SMH stack
- `BurntHouseRecords_schema.md` — Burnt House Records stack
- *(and so on for new clients as they're added)*

This `schema.md` only covers tools that **Coates Media itself owns and operates** — Mercury Banking, Zoho Books, the cPanel hosting account, the Hetzner box at `ops.coatesmedia.co`, etc. When Claude (or any AI) is doing work for a specific client, that client's `schema.md` is the source of truth for their stack.

---

## Services Offered

Coates Media is a **full-stack marketing and tech studio** for service-based businesses. Lexi blends creative and technical work into one offering — design, strategy, code, automation, and operations all from a single operator.

Service categories:

- **Marketing automation buildout** — n8n / Zapier / Zoho Flow infrastructure, lead routing, lifecycle workflows
- **CRM architecture & implementation** — Zoho One stack design, custom Creator apps, Deluge functions, picklist hygiene, attribution architecture
- **Data analytics & reporting** — SQL-heavy reporting (Zoho Analytics), custom dashboards, attribution analysis
- **Web design & development** — full builds on WordPress / Elementor and modern static stacks (Astro, Next.js); responsive, fast, deployment-ready
- **Photography & videography** — for clients who need it
- **Marketing strategy & operations** — paid media management (Google Ads, Meta), conversion tracking, lifecycle email/SMS via Zoho Campaigns
- **Custom integrations & app development** — Meta apps (Lead Sync), Google Cloud apps, browser automation (Playwright), API integrations across platforms

Lexi's positioning is "wears many hats by design" — clients hire Coates Media instead of needing to coordinate a designer + developer + marketer + ops person separately.

---

## Clients (Public)

The public client list — work Lexi is comfortable referencing on the website, in proposals, and in case studies.

### Active

| Client | Industry | Engagement type |
|---|---|---|
| **Fred Astaire Dance Studios (Philip Gutierrez Studio Group)** | Dance studio franchise (multi-location) | Full marketing operations, automation stack, CRM architecture, attribution audit |
| **OsteoStrong** | Wellness / fitness | [FILL: engagement type] |
| **Masakali** | [FILL: industry] | [FILL: engagement type] |
| **Sarah Michelle Hair** | Salon / beauty | Website hosting + maintenance |
| **Burnt House Records** | Recording studio / mixing & mastering | [FILL: engagement type — confirm with Lexi] |

### Past

| Client | Notes |
|---|---|
| **Pokii Eatery** | Food service. Past client, completed engagement. |

### Owned brands (Coates Media operates marketing / ops for these)

| Brand | Notes |
|---|---|
| **Thread Lightly** | Lexi's screen-printing / merch side business. CM runs all marketing, web, and ops for it. |

### Confidential / not-for-public-listing

[FILL: any clients you DON'T want referenced publicly even if AI generates copy]

---

## Conventions

### Meta App naming + ownership

- **Default:** Each client's Meta integrations live as a separate Meta App, ideally **owned by the client under their own Meta Business Manager** with Coates Media added as developer/admin.
- **Exception:** When the client doesn't want to manage Meta themselves (current case: FADS), the app lives under Coates Media's Meta Business with namespaced policy URLs.
- **Never:** A single mega-app spanning multiple clients. Blast radius too large; Meta policies don't support it well; per-client privacy policies become impossible to maintain.

### Meta App naming pattern

`<Client Brand Name> <App Description>` — e.g., `FADS Lead Sync`, `OsteoStrong Conversions`, etc.

### Privacy / ToS / Data Deletion URL pattern

Master pages live at the root:
- `coatesmedia.co/privacy` — master privacy policy
- `coatesmedia.co/terms` — master terms of service
- `coatesmedia.co/data-deletion` — master data deletion entry point with links to per-app pages

App-specific addenda live at:
- `coatesmedia.co/<client-slug>-<app-slug>/data-deletion`
- e.g., `coatesmedia.co/fads-lead-sync/data-deletion`

This keeps the legal infrastructure scalable: master + per-app addendum pattern means new client apps only require a new addendum file, not a rewrite of the master docs.

### Project folder convention

Lexi uses two parallel folder trees:
- `/Users/ancoates/Documents/Business/Coates Media/` — actual business work (Branding assets, Website code, AIContext docs, client subfolders)
- `/Users/ancoates/Documents/Claude/Projects/` — projects intended for Claude / Cowork access

Where overlap exists, the Business folder is the canonical location.

### Domain & SSL strategy (target)

Migrate all SSL away from GoDaddy (overpriced) toward Namecheap. Domain registrations can stay at GoDaddy or migrate as renewals come up.

### Hosting strategy (target)

Move client websites and Coates Media's own site off cPanel toward modern static stacks (Astro, Next.js) on Cloudflare Pages or Vercel where it makes sense. cPanel stays for clients with WordPress dependencies.

---

## Maintenance

This document is maintained by Lexi. Update when:

- A new client is added or moved between active/past (and create that client's own `<Client>_schema.md`)
- A new domain is registered
- A new operational tool is adopted (or one is dropped)
- A client adds or removes tooling that Lexi has access to (update their `<Client>_schema.md`, not this file)
- Meta App namespacing convention evolves
- Hosting / SSL / email setup changes

When updates affect AI workflows or shared context with other agents (Claude Code sessions, n8n workflows, Philip's agents), propagate the changes to:
- This file
- Lexi's session memory
- Any AI prompts or workflow context that reference Coates Media operational details

### Open items / FILL placeholders

- Engagement type details for each active client (OsteoStrong, Masakali)
- Industry tag for Masakali
- EIN if relevant
- Confidential client list if any
- Voice example phrases beyond what's in brand.md
