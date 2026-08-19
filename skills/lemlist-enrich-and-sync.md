---
name: lemlist-enrich-and-sync
description: Run lemlist's asynchronous enrichment (email, phone, LinkedIn) on one contact or in bulk, poll for the result, and land it on a lead or a CRM contact — with the credit accounting stated up front.
api: openapi/lemlist-enrich-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/lemlist-openapi-v2.json + https://developer.lemlist.com/skill.md
operations:
  - POST /enrich
  - POST /v2/enrichments/bulk
  - POST /leads/{leadId}/enrich
  - GET /enrich/{enrichId}
  - GET /team/credits
  - POST /contacts
  - GET /contacts/lists
  - PATCH /leads/{leadId}/variables
---

# Enrich contacts with lemlist

Base URL `https://api.lemlist.com/api`. Auth: HTTP Basic, **empty username**, API key
as the password.

**Enrichment costs money.** 5 credits per verified email, 20 per phone number, at
$0.01 per credit. Check the balance and say the number out loud before you spend it.

## 1. Check the budget

`GET /team/credits` returns the remaining balance and its breakdown. If the job you
are about to run costs more than the balance, stop and tell the user — the API will
answer `402 Payment Required` otherwise.

## 2. Submit the job

Enrichment is **asynchronous**: you submit, you get an id, you poll.

- `POST /enrich` — one input (email, name + company, or LinkedIn URL). Returns an
  enrichment id.
- `POST /v2/enrichments/bulk` — up to **500** inputs in one call.
- `POST /leads/{leadId}/enrich` — enrich a lead already in a campaign, in place.

## 3. Poll for the result

`GET /enrich/{enrichId}`. Poll every **5–10 seconds**; results typically arrive within
30 seconds. The response carries `status` plus the resolved `email`, `phone`,
`firstName`, `lastName`, `companyName`, `linkedinUrl` and the `credits` actually
consumed.

**Prefer webhooks over polling for bulk work.** Subscribe to `enrichmentDone` and
`enrichmentError` with `POST /hooks` and let lemlist call you — that is one request
instead of hundreds against a 20-per-2-seconds budget. See
`asyncapi/lemlist-webhooks.yml` for the full event catalog and the payload envelope.

## 4. Land the data

- On a **lead** (campaign-scoped): `POST /leads/{leadId}/variables` adds custom
  variables, `PATCH /leads/{leadId}/variables` updates them,
  `DELETE /leads/{leadId}/variables` erases the values. Use custom variables to carry
  your CRM's record id so the two systems stay joinable.
- On a **contact** (CRM-scoped, team-wide): `GET /contacts/lists` lists the CRM lists,
  `POST /contacts` adds or updates a contact, and
  `POST /contacts/lists/{listId}/entities` moves contacts in and out of a list.
  `GET /contacts/export` exports a list.
- Company-side: `POST /companies` adds or updates a company,
  `POST /companies/{companyId}/notes` attaches a note.

A lead and a contact are **different objects**. Pushing leads to contacts creates a
copy; nothing is moved and nothing is kept in sync afterwards.

## 5. Watch for rejected fields

`Contact` and `Company` both carry a `fieldRejections[]` array — `field`, `reason`,
`source`, `conflictingRecordId`, `rejectedValue`, `rejectedAt`. If an enrichment
appears not to have landed, read that array before re-running the job and paying
again.

## Failure handling

- `402` — out of credits. Do not retry; recharge first.
- `429` — 20 requests per 2 seconds per key. Honour `Retry-After`.
- `5xx` on a `POST` — **do not blind-retry**. lemlist publishes no idempotency key, so
  a replayed enrichment can be billed twice. Poll `GET /enrich/{enrichId}` with the id
  you already hold, or re-query the lead, before resubmitting.
