---
name: lemlist-monitor-and-reply
description: Watch campaign performance, subscribe to the right lemlist webhook events, and answer replies across email, LinkedIn and WhatsApp from the unified inbox.
api: openapi/lemlist-inbox-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/lemlist-openapi-v2.json + https://developer.lemlist.com/api-reference/endpoints/webhooks/add-webhook
operations:
  - GET /campaigns
  - GET /v2/campaigns/{campaignId}/stats
  - POST /v2/campaigns/stats/batch
  - GET /campaigns/reports
  - GET /inbox
  - GET /inbox/{contactId}
  - POST /inbox/email
  - POST /inbox/linkedin
  - POST /inbox/whatsapp
  - POST /hooks
  - GET /hooks
  - POST /leads/interested/{leadIdOrEmail}
---

# Monitor lemlist campaigns and answer replies

Base URL `https://api.lemlist.com/api`. Auth: HTTP Basic, **empty username**, API key
as the password.

## Measure

- `GET /campaigns` — list campaigns, filterable by status. Pass `version=v2` where the
  reference tells you to; some list endpoints still default to the deprecated v1.
- `GET /v2/campaigns/{campaignId}/stats` — statistics for one campaign over a date
  range.
- `POST /v2/campaigns/stats/batch` — statistics for many campaigns in **one** request.
  Prefer this over a loop: the rate limit is 20 requests per 2 seconds and a
  per-campaign loop burns it fast.
- `GET /campaigns/reports` — aggregated reports across campaigns.
- Large pulls: `GET /campaigns/{campaignId}/export/start` kicks off an asynchronous
  CSV export, `GET /campaigns/{campaignId}/export/{exportId}/status` polls it, and
  `PUT /campaigns/{campaignId}/export/{exportId}/email/{email}` sets the notification
  address. `GET /campaigns/{campaignId}/export/leads` exports the leads themselves.

Track sent, opened, clicked, replied, bounced and unsubscribed. A rising bounce rate
is a deliverability problem, not a copy problem — see the Deliverability alerts
surface (`POST /deliverability/alerts`) and lemwarm
(`GET /lemwarm/{userMailboxId}/settings`).

## Subscribe instead of polling

`POST /hooks` creates a webhook; `GET /hooks` lists them; `DELETE /hooks/{hookId}`
removes one. A webhook can be team-wide or bound to one campaign.

Pick the narrowest events you need. The catalog has 76 of them — the full list, the
payload envelope and the deprecations are in `asyncapi/lemlist-webhooks.yml`.
Useful starting points:

| Goal | Events |
|---|---|
| Positive replies | `warmed`, `interested`, `emailsReplied`, `linkedinReplied`, `whatsappReplied` |
| Deliverability trouble | `emailsBounced`, `emailsFailed`, `connectionIssue`, `customDomainErrors`, `sendLimitReached`, `deliverabilityAlertTriggered` |
| Enrichment jobs | `enrichmentDone`, `enrichmentError` |
| Buying signals | `signalRegistered` |

Set the optional `secret` on creation. lemlist stores it encrypted, never returns it
from any endpoint, and echoes it back in every callback body so you can verify the
call came from lemlist. It is **immutable** — rotating it means deleting and
recreating the webhook. Note that this is a shared secret in the body, not an HMAC
signature, so there is no replay protection: dedupe on the payload's `_id`.

Do not subscribe to `skipped`, `emailsSendFailed` or `opportunitiesDone` — they are
removed. Use `emailsFailed` and `annotated` instead.

## Reply

- `GET /inbox` — list unified-inbox conversations, filterable by channel and status.
- `GET /inbox/{contactId}` — read the thread before you answer. Always read it: the
  reply you are about to send is going to a real person mid-conversation.
- `POST /inbox/email`, `POST /inbox/linkedin`, `POST /inbox/whatsapp` — send on the
  channel the lead used.
- Drafts: `POST /inbox/{contactId}/drafts` creates one,
  `PATCH /inbox/{contactId}/drafts/{draftId}` edits it. **Draft first and let a human
  approve** when the reply commits the sender to anything.
- Labels: `POST /inbox/labels`, then
  `POST /inbox/conversations/labels/{contactId}` to attach.

## Close the loop

- `POST /leads/interested/{leadIdOrEmail}` / `POST /leads/notinterested/{leadIdOrEmail}`
  — or the campaign-scoped variants under
  `/campaigns/{campaignId}/leads/{leadIdOrEmail}/interested`.
- `POST /leads/pause/{leadId}` and `POST /leads/start/{leadId}` pause and resume a
  single lead without touching the campaign.
- Honour opt-outs immediately: `POST /unsubscribes/{email}` adds an email or a whole
  domain, and the v2 surface under `/v2/unsubscribes/` handles contact- and
  variable-level suppression. `DELETE /campaigns/{campaignId}/leads/` unsubscribes a
  lead from one campaign.

## Rules

- 20 requests per 2 seconds per API key. `429` carries `Retry-After` in seconds.
- No idempotency key: never blind-retry a `POST` — a retried inbox send is a second
  message to a real prospect.
- Errors are plain-text strings, not `problem+json`. `400 Bad team` means the key does
  not own the resource.
