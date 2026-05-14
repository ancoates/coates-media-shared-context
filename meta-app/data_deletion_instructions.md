# Data Deletion Instructions — FADS Lead Sync

**Last Updated:** 2026-05-07

This page describes how to request deletion of personal data processed by **FADS Lead Sync** (Meta App ID: 963876983267406).

---

## What this covers

This deletion process applies to lead data submitted through Meta (Facebook or Instagram) Lead Ad forms associated with Fred Astaire Dance Studios Pages. If you submitted such a form and want your information removed from our systems, follow the steps below.

---

## How to request deletion

Send an email to **ancoates@coatesmedia.co** with:

- **Subject line:** `Data Deletion Request — FADS Lead Sync`
- **Body must include:**
  - The email address you used when submitting the lead form
  - Your full name as submitted on the form (helps us locate the record if multiple submissions share the email)
  - The approximate date you submitted the form (optional but speeds up the process)
  - The studio location, if you remember it (e.g., Richmond, Cypress, Memorial)

You do not need to provide a reason. We will not contact you to verify or persuade against deletion.

---

## What gets deleted

Within **30 days** of receiving your verified request, we will:

1. **Delete your Lead record from the FADS Zoho CRM**, including: name, email, phone, all form responses, and any notes or attribution data associated with your record
2. **Notify the relevant FADS studio** that the record has been removed so they no longer attempt outreach
3. **Confirm completion** by replying to your request email

---

## What does NOT get deleted

The following are outside our control and require separate requests:

| Data | Where to request deletion |
|---|---|
| The Meta Lead Ad submission record itself | Submit a Meta data deletion request via your Facebook or Instagram account settings — Settings → Your Information → Download Your Information / Delete Your Information |
| Email or text messages a FADS studio sent to you using your information | Reply STOP to text messages, or unsubscribe from any email — and email the relevant studio directly |
| Records held by individual FADS studios in their own systems if they exported your data | Contact the studio directly |

---

## Verification

To prevent unauthorized deletion requests, we may verify your identity by sending a one-time confirmation email to the address on the lead record. You'll need to click a confirmation link in that email before deletion proceeds.

If we cannot verify the request, we will respond explaining why and request additional information.

---

## What if I never submitted a FADS lead form?

If you receive correspondence from a FADS studio but do not recall submitting any form, you may still request data deletion using the steps above — we will search by email and remove any matching records. Note that if your information was provided to a studio through a different channel (in person, phone call, referral), we may not have a record to delete via this process; in that case, please contact the studio directly.

---

## Automated callback (for Meta Platform integration)

For users of Facebook or Instagram who request deletion through Meta's account deletion flow, our system supports the Meta Data Deletion Callback at:

**Callback URL:** `https://ops.coatesmedia.co/webhook/fads.meta.deletion`

When Meta sends a deletion request to this endpoint, we automatically:

1. Validate the signed request from Meta
2. Locate the Lead record in Zoho CRM by Meta user ID
3. Delete the record within 30 days
4. Return a confirmation URL Meta can use to verify deletion status

Users can check the status of automated deletion via Meta's user-facing deletion confirmation page.

---

## Contact

For questions about data deletion or this process:

- **Email:** ancoates@coatesmedia.co
- **Subject line:** `Data Deletion Question — FADS Lead Sync`

For general privacy questions, see our Privacy Policy at https://coatesmedia.co/privacy. The FADS Lead Sync application is covered as Addendum A within that master policy.

---

*These instructions are published at https://coatesmedia.co/fads-lead-sync/data-deletion*
