---
name: lemlist-launch-campaign
description: Source leads from the lemlist B2B database, create a campaign with a sequence, add the leads, and start outreach — grounded in the operations lemlist's published OpenAPI actually declares.
api: openapi/lemlist-campaigns-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/lemlist-openapi-v2.json + https://developer.lemlist.com/skill.md
operations:
  - searchPeopleDatabase
  - POST /campaigns
  - POST /sequences/{sequenceId}/steps
  - POST /campaigns/{campaignId}/leads/
  - GET /campaigns/{campaignId}/statutes
  - POST /campaigns/{campaignId}/start
  - GET /team/credits
---

# Launch a lemlist campaign

Base URL `https://api.lemlist.com/api`.
Auth: `Authorization: Basic base64(":YOUR_API_KEY")` — **empty username**, the API key
is the password, and the leading colon is required. Bearer tokens are rejected.

> lemlist's own guidance for agents is to prefer its MCP server
> (`https://app.lemlist.com/mcp`) over the REST API. Use this skill when you are
> calling REST directly — from a script, a backend, or the `lemlist` CLI.

## Before you start

1. `GET /team/credits` — read the remaining credit balance. Enrichment on lead
   creation (`findEmail`, `findPhone`, `linkedinEnrichment`) spends credits: 5 per
   verified email, 20 per phone number. **Tell the user the cost before you spend it.**
2. Confirm the team has at least one connected sending channel. `GET /team/senders`
   lists team members and their campaigns; `GET /user/channels` returns the connected
   email / LinkedIn / WhatsApp channels for the authenticated user.

## Steps

### 1. Find the leads

`POST /database/people` (`operationId: searchPeopleDatabase`) searches the lemlist
people database by role, industry, company size and location. `GET /database/filters`
returns the filters you may set. Save a repeatable search as a persona with
`POST /database/personas` (`operationId: createPersona`).

### 2. Create the campaign

`POST /campaigns` creates the campaign **together with an auto-generated sequence and
schedule**. Keep the returned `_id` (a `cam_…` id) and the `sequenceId`.

Some list endpoints still default to the deprecated v1 behaviour — send
`version=v2` as a query parameter where the reference tells you to.

### 3. Write the sequence

`POST /sequences/{sequenceId}/steps` adds each step (email, LinkedIn, call, task,
delay). `PATCH /sequences/{sequenceId}/steps/{stepId}` edits one.
`GET /campaigns/{campaignId}/sequences` reads the whole sequence back.

To A/B test an email step: `POST /sequences/{sequenceId}/steps/{stepId}/ab-test`
creates variant B prefilled from variant A, and
`POST /sequences/{sequenceId}/steps/{stepId}/ab-test/winner` ends the test.

Store `stepId`, not `sequenceStep` — `sequenceStep` is a position that shifts when the
sequence is reordered.

### 4. Add the leads

`POST /campaigns/{campaignId}/leads/` creates a lead in the campaign. The enrichment
query flags on this operation are the credit-bearing ones. `deduplicate` and
`notInAnyCampaign` guard against contacting the same person twice.

A **lead** belongs to a campaign; a **contact** lives in the CRM. They are separate
objects — `POST /contacts` copies data across, it does not move it.

### 5. Check before launching

`GET /campaigns/{campaignId}/statutes` returns validation statutes: errors that block
launch, and warnings about daily limits and DNS issues. Read it and report anything
it flags.

### 6. Start it

`POST /campaigns/{campaignId}/start`. **Never start, pause or delete a campaign
without explicit user confirmation** — lemlist says so in its own agent guidance, and
a campaign that starts by accident sends real email to real people.

`POST /campaigns/{campaignId}/pause` stops it again without affecting scheduled leads.

## Rules that apply to every call

- **Rate limit** — 20 requests per 2 seconds, per API key, on all routes. Read
  `X-RateLimit-Remaining`; on `429` honour `Retry-After` (seconds) and back off.
  `X-RateLimit-Reset` is a **human-readable date string**, not an epoch.
- **No idempotency key.** lemlist publishes none. Retry `GET`/`PUT`/`DELETE` freely,
  but never blind-retry a `POST` or `PATCH` after a 5xx or a network drop — the write
  may already have landed. This is exactly the rule lemlist's own CLI follows.
- **Errors** are mostly plain-text strings, not `problem+json`. `400` is commonly
  `Bad team` (wrong team for this key) or `Bad params`. `402` means you ran out of
  credits. `401` means the Basic header is wrong — check the leading colon.
- **One credential = one team.** There is no team selector; to act for another
  account, use that account's key.
