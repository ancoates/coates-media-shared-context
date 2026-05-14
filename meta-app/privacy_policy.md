# Privacy Policy — Coates Media

**Last Updated:** 2026-05-07

This Privacy Policy describes how **Coates Media LLC** ("we," "us," or "our") collects, uses, and protects personal information across our websites, applications, and services, including any third-party platform applications we operate (collectively, the "Services").

This is a master privacy policy. App-specific or service-specific data handling details, where they differ from this policy, are described in the Addenda at the end of this document.

---

## 1. Who we are

| Item | Detail |
|---|---|
| Operating entity | Coates Media LLC |
| Business address | 3416 41st St, Lubbock, TX 79413 |
| Privacy contact | ancoates@coatesmedia.co |
| Website | https://coatesmedia.co |

For privacy questions, requests, or to exercise your rights under this policy, email **ancoates@coatesmedia.co**.

---

## 2. Scope

This policy applies to:

- The Coates Media website (`coatesmedia.co`) and any subdomains we operate
- Marketing automation services we provide to our clients (currently including Fred Astaire Dance Studios franchise locations)
- Third-party platform applications we operate, including but not limited to:
  - **FADS Lead Sync** — Meta Platforms application (App ID: 963876983267406) that processes Lead Ad submissions for Fred Astaire Dance Studios franchise locations

Where an individual app or service has data flows or retention practices that differ from this master policy, those differences are described in the Addenda below.

---

## 3. What data we collect

We collect personal information in the following ways:

**Directly from you:**
- When you contact us via email, web form, or other channels
- When you sign up for newsletters, demos, or marketing communications
- When you become a client or vendor

**Through our applications and services:**
- Lead data submitted through Meta Lead Ads or other ad platforms operated on behalf of our clients
- Form submissions on websites we operate or manage
- Identifiers required for ad attribution (e.g., click IDs, campaign IDs, ad IDs)

**Automatically:**
- Standard web analytics data (pages visited, browser type, IP address) on our own websites
- Performance and usage telemetry from our applications, in aggregate

We do not collect: government identifiers, payment account numbers, biometric data, precise geolocation beyond city/region voluntarily submitted, or health data.

---

## 4. How we use the data

We process personal data to:

1. Deliver the services our clients hire us to provide (e.g., routing leads to the correct studio CRM, attributing marketing performance, supporting customer follow-up)
2. Operate and improve our websites and applications
3. Communicate with you about Coates Media services if you've expressed interest
4. Comply with legal obligations (tax records, regulatory inquiries, etc.)

We do not sell personal data. We do not share lead data with advertisers, data brokers, or marketing platforms outside the scope of the service we are operating.

---

## 5. Where data is stored

| Type | Where |
|---|---|
| Lead data routed to client CRMs | Stored in the client's CRM (e.g., Zoho CRM for FADS franchise locations) |
| In-transit processing | Coates Media automation infrastructure at `ops.coatesmedia.co` (transient, less than 60 seconds, no persistent storage) |
| Coates Media operational records | U.S.-based cloud providers (Zoho, Mercury, Stripe) |

All data is encrypted in transit (HTTPS / TLS) and at rest using each provider's standard encryption. Sub-processors include Zoho Corporation (CRM), and on a per-service basis as listed in the Addenda.

---

## 6. How long we keep data

| Stage | Retention |
|---|---|
| In-transit through `ops.coatesmedia.co` | < 60 seconds (no persistent storage) |
| Operational logs (n8n execution history) | 30 days, then auto-purged |
| Lead records in client CRMs | Per client's retention policy; typically until the lead is converted, marked Lost, or deletion is requested |
| Customer / business records | Up to 7 years for legitimate business purposes (tax, contracts, regulatory compliance) |

If a Lead is converted to a Contact (e.g., a paying student at a FADS studio), the record is retained for the duration of the customer relationship and a reasonable period thereafter, consistent with U.S. business records norms.

---

## 7. Who we share data with

We share personal data only with:

1. **The client whose service the data was collected on behalf of.** Lead data submitted through ads operated for a specific client flows only to that client's CRM and is accessible only by that client's authorized staff.
2. **Sub-processors** acting under a Data Processing Agreement (e.g., Zoho Corporation as CRM provider).
3. **Authorities or legal entities** if compelled by law (subpoena, court order). We will provide notice to the affected individual where legally permissible.

We do not sell or rent personal data. Aggregated, de-identified data may be used for performance reporting and product improvement.

---

## 8. Your rights

You may request, at no charge:

- **Access** to the personal data we hold about you
- **Correction** of inaccurate data
- **Deletion** of your data (see Section 9)
- **Restriction** of processing
- **Objection** to processing for marketing purposes
- **Data portability** — a machine-readable copy of your data

To exercise any of these rights, email **ancoates@coatesmedia.co** with subject line `Privacy Request` and include the email address associated with the data. We will respond within 30 days.

---

## 9. Data deletion

To request deletion of your personal data, follow the instructions at:

**https://coatesmedia.co/data-deletion**

For app-specific deletion processes (e.g., Meta Platform integrations), see the Addenda.

---

## 10. Security

We protect personal data through:

- HTTPS / TLS encryption for all data in transit
- OAuth 2.0 token-based authentication for all CRM, advertising, and platform API access
- Role-based access controls within client CRMs, scoped to the appropriate audience
- Audit logs of administrative access
- Encryption at rest in our cloud providers

We follow industry-standard practices but cannot guarantee absolute security. If we become aware of a breach affecting your data, we will notify you in accordance with applicable law.

---

## 11. Children

Our services are not intended for use by individuals under 13 years of age. We do not knowingly collect data from children under 13. If we discover such collection has occurred inadvertently, we will delete it.

Some of our clients (e.g., dance studios) offer programs for children 13+; in those cases, ad lead forms are completed by a parent or guardian on the child's behalf, and the data we receive is the parent's contact information.

---

## 12. International users

Coates Media operates in the United States. Data is processed and stored in U.S.-based infrastructure. If you submit data from outside the U.S., it will be transferred to the U.S. for processing. By using our services or submitting data through our platforms, you consent to this transfer.

---

## 13. Changes to this policy

We may update this Privacy Policy periodically. The "Last Updated" date at the top reflects the most recent revision. Material changes (e.g., new categories of data collected, new sub-processors) will be communicated to active contacts at the email on file.

---

## 14. Contact

| Channel | Contact |
|---|---|
| Privacy questions, requests, deletion | ancoates@coatesmedia.co |

---

# Addenda — Application-Specific Notes

---

## A. FADS Lead Sync (Meta Platforms App)

| Item | Detail |
|---|---|
| App name | FADS Lead Sync |
| Meta App ID | 963876983267406 |
| Use case | Capture & manage ad leads with Marketing API |
| Operating entity | Coates Media LLC |

**What it does:** Receives Meta (Facebook / Instagram) Lead Ad submissions from Pages associated with Fred Astaire Dance Studios franchise locations, and routes that data to the FADS Zoho CRM so the relevant studio can follow up.

**Data collected:** First name, last name, email, phone, any additional questions configured on the lead form, and Meta-supplied identifiers (`leadgen_id`, `form_id`, `ad_id`, `campaign_id`, Page ID).

**Data flow:** Meta → `ops.coatesmedia.co` (transient, <60 seconds) → Zoho CRM (persistent storage). Encryption in transit and at rest.

**Authorized Pages:** Currently the eleven FADS Pages listed in the Application's Terms of Service. Additional Pages require explicit authorization.

**Deletion process specific to this app:** See https://coatesmedia.co/fads-lead-sync/data-deletion. Includes Meta Data Deletion Callback support at `https://ops.coatesmedia.co/webhook/fads.meta.deletion`.

---

*This policy is published at https://coatesmedia.co/privacy*
