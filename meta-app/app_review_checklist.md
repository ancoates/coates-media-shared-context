# Meta App Review — Submission Checklist (FADS Lead Sync)

**App ID:** 963876983267406
**App Name:** FADS Lead Sync
**Use Case:** Capture & manage ad leads with Marketing API
**Goal:** Take the app from Development → Live so production lead delivery works for all 11 FADS studio Pages.

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
| `ads_read` | ❌ Drop | Campaign IDs come from the lead webhook payload itself |
| `ads_management` | ❌ Drop | Only needed to write ads; receiver doesn't |

**To drop them:** App Dashboard → App Review → Permissions and Features → find each unwanted permission → Remove. Each removed permission also removes its "1 API call required" gate.

The big remaining gate: **Marketing API Access Tier — 500 calls @ 85% success rate.** Worth checking with Meta docs whether `GET /<leadgen_id>` counts toward Marketing API tier or just Graph API. If it's only Graph API, the 500-call gate may not apply at all.

---

## Step 2 — Publish the policy URLs

Three pages need to live at publicly accessible URLs before submitting:

| Document | Source file (this folder) | Target URL on coatesmedia.co |
|---|---|---|
| Privacy Policy | `privacy_policy.md` | `https://coatesmedia.co/fads-lead-sync/privacy` |
| Terms of Service | `terms_of_service.md` | `https://coatesmedia.co/fads-lead-sync/terms` |
| Data Deletion Instructions | `data_deletion_instructions.md` | `https://coatesmedia.co/fads-lead-sync/data-deletion` |

**Before publishing, fill in:**

- Privacy Policy → `[INSERT BUSINESS ADDRESS]` placeholder
- Verify `privacy@coatesmedia.co`, `legal@coatesmedia.co`, and `hello@coatesmedia.co` mailboxes exist (or update to addresses you actually monitor)
- Confirm "Coates Media Marketing" is the right legal entity name (vs. Coates Media, vs. Lexi Coates DBA, etc.)
- Confirm Texas / Harris County is the right governing-law jurisdiction in the ToS

Quick implementation options if coatesmedia.co is WordPress:
- Add three new Pages with the markdown content rendered as HTML
- Or link to the markdown files directly hosted as public Gists or in a static site

---

## Step 3 — App Dashboard configuration

| Setting | Where | Value |
|---|---|---|
| Privacy Policy URL | App Settings → Basic | `https://coatesmedia.co/fads-lead-sync/privacy` |
| Terms of Service URL | App Settings → Basic | `https://coatesmedia.co/fads-lead-sync/terms` |
| Data Deletion Instructions URL | App Settings → Basic → Data Deletion Instructions URL | `https://coatesmedia.co/fads-lead-sync/data-deletion` |
| App Icon | App Settings → Basic | 1024×1024 PNG (Coates Media or FADS-related branding) |
| Category | App Settings → Basic | Business and Pages |
| App Domain | App Settings → Basic | `coatesmedia.co` |
| Business Verification | App Settings → Business Verification | Submit Coates Media Marketing's business documentation |

---

## Step 4 — Demo screencast

Meta requires a video showing the app's actual data flow for the `leads_retrieval` permission. Suggested flow (~2 min):

1. **0:00–0:15** — Open Lead Ads Testing Tool, select a FADS Page, fire a test submission
2. **0:15–0:45** — Switch to n8n Executions tab, show the workflow run end-to-end (Meta Webhook → Verify + Parse → Fetch Lead from Meta → Build Zoho Payload → Zoho Upsert)
3. **0:45–1:15** — Open the Build Zoho Payload node output to show the structured lead data being formatted
4. **1:15–1:45** — Switch to Zoho CRM, open Leads, search for the test lead's email, show the populated record (Studio, Lead_Source, Channel, Platform, Meta IDs)
5. **1:45–2:00** — Voiceover summary: "FADS Lead Sync receives Meta Lead Ad submissions and routes them to our Zoho CRM so studio staff can follow up. No data is sold or shared with third parties outside our CRM."

Tools: QuickTime screen recording on Mac. Keep it under 3 minutes; Meta reviewers don't watch long videos.

---

## Step 5 — Permission justifications (text Meta will read)

For each permission still requested, paste the following text into the Permission Justification field during App Review submission.

### `leads_retrieval`

> FADS Lead Sync uses leads_retrieval to fetch the full content of Meta Lead Ad submissions on behalf of Fred Astaire Dance Studios franchise locations. When a user submits a Lead Ad form on a FADS studio's Page, our application receives a leadgen webhook event containing the leadgen_id, then calls GET /{leadgen_id} to retrieve the user's name, email, phone, and other form responses. This data is written to the FADS Zoho CRM so the relevant studio can follow up. The integration replaces a third-party Zapier automation and reduces the time between lead submission and studio outreach.

### `pages_show_list`

> FADS Lead Sync uses pages_show_list to enumerate the eleven Fred Astaire Dance Studios Pages owned or managed by Coates Media Marketing. We use this once during initial setup to derive a Page Access Token for each Page and to confirm which Pages should subscribe to leadgen webhooks.

### `pages_read_engagement`

> FADS Lead Sync uses pages_read_engagement to receive the leadgen webhook field for FADS Pages. Without this permission, Meta would not deliver leadgen events to our webhook URL.

### `pages_manage_metadata`

> FADS Lead Sync uses pages_manage_metadata to call POST /{page_id}/subscribed_apps for each FADS Page during setup. This subscribes our app to receive leadgen webhook events from each Page. We do not modify any other page metadata; we only manage the app subscription for webhook delivery.

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
- ⏸ Demo video: deferred — will record after Coates Media website overhaul lands

## Architectural decisions (2026-05-07)

**Master policies + addenda pattern:**
- Single Privacy Policy at `https://coatesmedia.co/privacy` covering all Coates Media services + apps
- Single Terms of Service at `https://coatesmedia.co/terms` likewise
- App-specific notes added as addenda within the master docs (FADS Lead Sync currently the only one)
- Future apps: just add new addenda, no new top-level docs needed

**Meta app strategy: one app per client, grow over time:**
- FADS Lead Sync = THE app for everything FADS (current = lead receiving; future = Messenger DM ingestion, ads insights, offline conversion uploads, etc.)
- Add new permissions to existing app via "permission update" review — much faster than full app review since business verification already done
- New clients (OsteoStrong, etc.) = new Meta app per client; do NOT cram multiple clients into one app (Meta forces "Tech Provider" review for that)

**Coates Media website overhaul = separate project:**
- New project folder: `Coates Media Website Overhaul/`
- Build with Claude Code (better suited for multi-page web project)
- Privacy + Terms + data deletion pages live in that project, hosted on coatesmedia.co
- This Sprint 2 work just produces the markdown source-of-truth files; the website project takes them and ships them

## Pre-submission checklist

- [ ] Coates Media website overhaul — publish `/privacy`, `/terms`, `/data-deletion`, `/fads-lead-sync/data-deletion`
- [ ] Set those URLs in the Meta App Dashboard → App Settings → Basic
- [ ] Drop unused Meta permissions (pages_manage_ads, business_management, ads_read, ads_management) per Step 1 above
- [ ] Pull App Icon from Coates Media branding, upload (1024×1024 PNG)
- [ ] Submit Business Verification (Coates Media LLC documentation)
- [ ] Record demo screencast (deferred until after website launch)
- [ ] Submit for App Review with the permission justifications in Step 5
