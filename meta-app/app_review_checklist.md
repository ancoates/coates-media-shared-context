# Meta App Review — Submission Checklist (Coates Media Connect)

**App ID:** 963876983267406
**App Name:** Coates Media Connect *(formerly "FADS Lead Sync" — renamed 2026-06-03 for multi-client use)*
**Use Case:** Capture & manage ad leads with Marketing API
**Goal:** Take the app from Development → Live so production lead delivery works for the first client's Pages (the 11 FADS studio Pages). Coates Media Connect is the agency's single consolidated Meta app; additional clients are added to the same app via partner sharing, not by creating new apps.

---

## Step 1 — Trim permissions before submitting (saves review time)

You currently have 9 permissions requested. The receiver only NEEDS 5. Drop the other 4 to reduce App Review burden:

| Permission | Required? | Rationale |
|---|---|---|
| `leads_retrieval` | ✅ Required | `GET /<leadgen_id>` to fetch full lead data |
| `pages_show_list` | ✅ Required | Enumerate the 11 FADS Pages your token can access |
| `pages_read_engagement` | ✅ Required | Receive `leadgen` webhook events |
| `pages_manage_metadata` | ✅ Required | Subscribe each Page to the app's webhook (`POST /<page_id>/subscribed_apps`) |
| `public_profile` | ✅ Default | Auto-included; no action needed |
| `pages_manage_ads` | ❌ Drop | Only needed to create/edit ads; receiver doesn't |
| `business_management` | ❌ Drop | You're using the personal-admin token path, not Business path |
| `ads_read` | ❌ Drop for now | Campaign IDs come from the lead webhook payload itself. Re-add **after** this review is Live, as a lighter permission-update review, to power the Meta change detector (`common/n8n-infra/meta-change-detector.md`). Do not bundle it into this first submission. |
| `ads_management` | ❌ Drop | Only needed to write ads; receiver doesn't |

**To drop them:** App Dashboard → App Review → Permissions and Features → find each unwanted permission → Remove. Each removed permission also removes its "1 API call required" gate.

The big remaining gate: **Marketing API Access Tier — 500 calls @ 85% success rate.** Worth checking with Meta docs whether `GET /<leadgen_id>` counts toward Marketing API tier or just Graph API. If it's only Graph API, the 500-call gate may not apply at all.

---

## Step 2 — Publish the policy URLs

Three pages need to live at publicly accessible URLs before submitting:

Canonical URLs are **app-neutral** (no per-app vanity slugs) so they survive the multi-client consolidation:

| Document | Source file (this folder) | Target URL on coatesmedia.co |
|---|---|---|
| Privacy Policy | `privacy_policy.md` | `https://coatesmedia.co/privacy` |
| Terms of Service | `terms_of_service.md` | `https://coatesmedia.co/terms` |
| Data Deletion Instructions | `data_deletion_instructions.md` | `https://coatesmedia.co/data-deletion` |

**Status (2026-06-03):** The Coates Media website is live and these pages are published. The legacy `/fads-lead-sync/*` slugs are retired — confirm the webdev agent renders the renamed content at the app-neutral URLs above and that no `/fads-lead-sync/*` route lingers. The master docs source from the `shared-context` submodule, so a pointer bump on coatesmedia.co picks up the rename.

---

## Step 3 — App Dashboard configuration

| Setting | Where | Value |
|---|---|---|
| Privacy Policy URL | App Settings → Basic | `https://coatesmedia.co/privacy` |
| Terms of Service URL | App Settings → Basic | `https://coatesmedia.co/terms` |
| Data Deletion Instructions URL | App Settings → Basic → Data Deletion Instructions URL | `https://coatesmedia.co/data-deletion` |
| App Icon | App Settings → Basic | 1024×1024 PNG (Coates Media branding) |
| Category | App Settings → Basic | Business and Pages |
| App Domain | App Settings → Basic | `coatesmedia.co` |
| Business Verification | App Settings → Business Verification | Submit Coates Media LLC's business documentation |

---

## Step 4 — Demo screencast

Meta requires a video showing the app's actual data flow for the `leads_retrieval` permission. Suggested flow (~2 min):

1. **0:00–0:15** — Open Lead Ads Testing Tool, select a FADS Page, fire a test submission
2. **0:15–0:45** — Switch to n8n Executions tab, show the workflow run end-to-end (Meta Webhook → Verify + Parse → Fetch Lead from Meta → Build Zoho Payload → Zoho Upsert)
3. **0:45–1:15** — Open the Build Zoho Payload node output to show the structured lead data being formatted
4. **1:15–1:45** — Switch to Zoho CRM, open Leads, search for the test lead's email, show the populated record (Studio, Lead_Source, Channel, Platform, Meta IDs)
5. **1:45–2:00** — Voiceover summary: "Coates Media Connect receives Meta Lead Ad submissions on behalf of the businesses we manage and routes each lead to that client's Zoho CRM so their staff can follow up. No data is sold or shared with third parties outside the client's CRM."

Tools: QuickTime screen recording on Mac. Keep it under 3 minutes; Meta reviewers don't watch long videos.

---

## Step 5 — Permission justifications (text Meta will read)

For each permission still requested, paste the following text into the Permission Justification field during App Review submission.

> Agency framing: justifications describe Coates Media Connect as the agency app operated on behalf of the client businesses Coates Media manages, beginning with Fred Astaire Dance Studios. Keep this framing consistent with the (now client-agnostic) app name — reviewers cross-check the name, the policy URLs, and this text.

### `leads_retrieval`

> Coates Media Connect uses leads_retrieval to fetch the full content of Meta Lead Ad submissions on behalf of the client businesses Coates Media manages, beginning with Fred Astaire Dance Studios franchise locations. When a user submits a Lead Ad form on a client's Page, our application receives a leadgen webhook event containing the leadgen_id, then calls GET /{leadgen_id} to retrieve the user's name, email, phone, and other form responses. This data is written to the relevant client's Zoho CRM so that client can follow up. The integration replaces a third-party Zapier automation and reduces the time between lead submission and outreach.

### `pages_show_list`

> Coates Media Connect uses pages_show_list to enumerate the client Pages that authorize Coates Media to manage them — currently the eleven Fred Astaire Dance Studios Pages. We use this once during setup to derive a Page Access Token for each authorized Page and to confirm which Pages should subscribe to leadgen webhooks.

### `pages_read_engagement`

> Coates Media Connect uses pages_read_engagement to receive the leadgen webhook field for the client Pages we manage. Without this permission, Meta would not deliver leadgen events to our webhook URL.

### `pages_manage_metadata`

> Coates Media Connect uses pages_manage_metadata to call POST /{page_id}/subscribed_apps for each authorized client Page during setup. This subscribes our app to receive leadgen webhook events from each Page. We do not modify any other page metadata; we only manage the app subscription for webhook delivery.

---

## Step 6 — Submit for review

App Dashboard → App Review → Permissions and Features → click "Submit for Review" at the top.

**Expected timeline:** 3–7 business days for Meta to review. They may request clarifications via email; respond promptly.

While waiting:

- ✅ Continue running Zapier in parallel
- ✅ Build out the other 10 Pages' Lead Access grants + subscriptions
- ✅ Prep the rest of Sprint 2 work (Google Lead Form receiver, GF universal receiver)
- ❌ Do NOT disable Zapier until App Review is approved AND a real production lead has flowed through n8n

---

## Step 7 — After approval

When Meta approves:

1. Run the `fads.meta.batch_subscribe_pages` workflow → all 11 Pages subscribed via API
2. Manually grant Lead Access for the 10 remaining Pages (Lead Access Manager UI; not API-able)
3. Wait 24–48 hours for organic Richmond + other-studio leads to flow through n8n
4. Confirm 5+ real leads have landed in Zoho cleanly across multiple studios
5. Disable (don't delete) the 26 Meta Lead Form Zapier zaps, keeping them as 1-week rollback option
6. After 1 week of clean operation, delete the Zapier zaps permanently

---

## Confirmed inputs (filled 2026-05-07)

- ✅ Legal entity: **Coates Media LLC**
- ✅ Address: **3416 41st St, Lubbock, TX 79413**
- ✅ Single contact email: **ancoates@coatesmedia.co**
- ✅ Master Privacy Policy + Terms (covers all Coates Media services + apps)
- ✅ App icon: pull from existing Coates Media branding when ready
- ⏸ Demo video: now unblocked (website is live) — record before submitting; use the Coates Media Connect framing in Step 4

## Architectural decisions (2026-05-07, revised 2026-06-03)

**Master policies + addenda pattern:**
- Single Privacy Policy at `https://coatesmedia.co/privacy` covering all Coates Media services + apps
- Single Terms of Service at `https://coatesmedia.co/terms` likewise
- App-specific notes added as addenda within the master docs (Coates Media Connect = Addendum A; Google Ads API integration = Addendum C)
- Future apps: just add new addenda, no new top-level docs needed

**Meta app strategy (REVISED 2026-06-03): one consolidated agency app for all clients.**

> This reverses the original 2026-05-07 "one app per client" decision. Rationale below.

- **Coates Media Connect** (App ID `963876983267406`, formerly "FADS Lead Sync") is THE single Meta app for all clients. Onboarding a new client = the client partner-shares their Pages/Ad Accounts into Coates Media's Business Portfolio + we run the subscribe workflow. No new app, no new business verification, no new review lifecycle.
- Grow capability via **permission-update reviews** on this one app (lighter than full review since business verification is already done): current = lead receiving; next = `ads_read` for the change detector; later = Messenger DM ingestion, offline conversion uploads (`ads_management`/CAPI), etc.
- **Why the reversal:** the original "split per client to avoid Tech Provider review" rationale was wrong. A Meta app is a Tech Provider the moment it touches data of a business that doesn't own the app — and the client Pages here live in the clients'/franchisees' (and Envision's) portfolios, not Coates Media's. So the app is *already* a Tech Provider app. Splitting per client does **not** dodge that classification (or the Data Protection Assessment that can accompany it); it only multiplies apps, verifications, and reviews. One agency app is strictly cheaper for the same cost, and it's how every agency lead-sync tool operates.
- Credential model: a System User in Coates Media's Business Portfolio issues tokens spanning all partner-shared client accounts. (The current leadform receiver still uses per-Page personal-admin tokens because some FADS Pages are stuck in Envision's defunct portfolio — keep those two credential paths separate.)

**Coates Media website (DONE 2026-06): live.**
- Privacy + Terms + data-deletion pages are published on coatesmedia.co, sourced from the `shared-context` submodule (`meta-app/*.md` here).
- Source-of-truth edits land here, in the upstream `coates-media-shared-context` repo, then propagate via submodule pointer bumps (see `shared-context-sync` playbook).

## Pre-submission checklist

- [x] Rename app to **Coates Media Connect** in the Meta dashboard (done 2026-06-03)
- [x] Website live — `/privacy`, `/terms`, `/data-deletion` published (app-neutral URLs)
- [ ] Confirm webdev rendered the renamed content + retired any `/fads-lead-sync/*` route (bump `shared-context` pointer in coatesmedia-web)
- [ ] Set `/privacy`, `/terms`, `/data-deletion` in the Meta App Dashboard → App Settings → Basic
- [ ] Drop unused Meta permissions (pages_manage_ads, business_management, ads_read, ads_management) per Step 1 above
- [ ] Pull App Icon from Coates Media branding, upload (1024×1024 PNG)
- [ ] Submit Business Verification (Coates Media LLC documentation)
- [ ] Record demo screencast (Coates Media Connect framing, Step 4)
- [ ] Submit for App Review with the permission justifications in Step 5
- [ ] **After Live:** add `ads_read` via permission-update review → build the Meta change detector
