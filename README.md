# lemlist

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

lemlist is a sales engagement and cold outreach platform from lempire that helps sales teams build prospect lists, personalize multichannel campaigns across email, LinkedIn, phone, SMS and WhatsApp, and automate follow-ups to book more meetings. It includes a 650M+ record B2B lead database, credit-metered email and phone enrichment, Signal Agents that watch for buying triggers, a unified reply inbox, and lemwarm deliverability warm-up. The developer surface is unusually agent-forward for its category - a 143-operation REST API documented with a published OpenAPI, a hosted remote MCP server at app.lemlist.com/mcp with OAuth 2.1 and dynamic client registration, an official OpenAPI-generated CLI on npm, an llms.txt index, a published Agent Skill, and a 76-event webhook catalog.

**Areas:** Email Outreach · Sales Engagement · Cold Email · Sales Automation · LinkedIn Outreach · Lead Generation · Data Enrichment · Deliverability · CRM · Multichannel Messaging · Webhook · MCP

## lemlist on APIs.io

Everything profiled for lemlist is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/lemlist/](https://apis.io/providers/lemlist/)** — or go straight to one of the APIs or properties below.

### APIs (22)

- [lemlist MCP Server](https://apis.io/apis/lemlist/mcp-server/) — lemlist's hosted remote Model Context Protocol server. An MCP client POSTs to https://app.lemlist.com/mcp and authenticates with OAuth 2.1 (authorization…
- [lemlist Campaigns API](https://apis.io/apis/lemlist/lemlist-campaigns-api/) — Campaign CRUD and lifecycle - create, update, duplicate, start, pause, validation statutes, stats, reports and asynchronous exports.
- [lemlist Sequences API](https://apis.io/apis/lemlist/lemlist-sequences-api/) — Campaign sequences, their steps, and A/B test variants on email steps.
- [lemlist Leads API](https://apis.io/apis/lemlist/lemlist-leads-api/) — Leads inside campaigns - create with optional enrichment, update, pause, resume, mark interested, custom variables, CRM import and unsubscribe.
- [lemlist People Database API](https://apis.io/apis/lemlist/lemlist-people-database-api/) — Search the lemlist B2B people and company database, list its filters, and manage saved personas.
- [lemlist Enrich API](https://apis.io/apis/lemlist/lemlist-enrich-api/) — Asynchronous enrichment - find and verify emails, phone numbers and LinkedIn data, single or in bulk, then poll for the result. Credit-metered.
- [lemlist Inbox API](https://apis.io/apis/lemlist/lemlist-inbox-api/) — The unified reply inbox - conversations, messages, drafts, labels and sending on email, LinkedIn and WhatsApp.
- [lemlist Contacts API](https://apis.io/apis/lemlist/lemlist-contacts-api/) — CRM-side contacts, contact lists, list membership and exports.
- [lemlist Companies API](https://apis.io/apis/lemlist/lemlist-companies-api/) — CRM-side companies and company notes.
- [lemlist Signal Agents API](https://apis.io/apis/lemlist/lemlist-signal-agents-api/) — Signal Agents (watch lists) - create and configure watches, list the available signal types and filters, read detected signals, and push external signals.
- [lemlist Webhooks API](https://apis.io/apis/lemlist/lemlist-webhooks-api/) — Webhook subscription management - list, create with an optional shared secret, and delete. 76 event types are documented.
- [lemlist Unsubscribes API](https://apis.io/apis/lemlist/lemlist-unsubscribes-api/) — Suppression management - unsubscribe and re-subscribe contacts and variables, list and export the suppression set, and the legacy email/domain surface.
- [lemlist Schedules API](https://apis.io/apis/lemlist/lemlist-schedules-api/) — Sending schedules - CRUD and association with campaigns.
- [lemlist Tasks API](https://apis.io/apis/lemlist/lemlist-tasks-api/) — Manual tasks - list, create, update and ignore.
- [lemlist Activities API](https://apis.io/apis/lemlist/lemlist-activities-api/) — The activity history feed, and deletion of call recordings and transcripts.
- [lemlist Team API](https://apis.io/apis/lemlist/lemlist-team-api/) — Team-level endpoints - team information, senders, remaining credits and CRM users.
- [lemlist Users API](https://apis.io/apis/lemlist/lemlist-users-api/) — User endpoints - user detail and the connected channels available to the authenticated user.
- [lemlist Email Accounts API](https://apis.io/apis/lemlist/lemlist-email-accounts-api/) — Connect, test and disconnect custom SMTP/IMAP sending accounts.
- [lemlist Lemwarm API](https://apis.io/apis/lemlist/lemlist-lemwarm-api/) — lemwarm mailbox warm-up - start, pause, and read or update warm-up settings per mailbox.
- [lemlist Deliverability Alerts API](https://apis.io/apis/lemlist/lemlist-deliverability-alerts-api/) — Threshold alerts on deliverability metrics - create, read, update and delete.
- [lemlist Fields API](https://apis.io/apis/lemlist/lemlist-fields-api/) — The custom field definitions available on leads, contacts and companies.
- [lemlist Stats API](https://apis.io/apis/lemlist/lemlist-stats-api/) — The Stats API from lemlist — 2 operation(s) for stats.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Lemlist Webhooks](https://apis.io/asyncapis/lemlist/lemlist-webhooks/)

#### GraphQL (1)

GraphQL schemas.

- [Moved to /providers/lemlist/](https://apis.io/graphqls/lemlist/lemlist-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [lemlist](https://apis.io/servers/lemlist/lemlist/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Lemlist Agentic Access](https://apis.io/agentic-access/lemlist/lemlist-agentic-access/)

#### Examples (1)

Example requests and responses.

- [Lemlist Examples](https://apis.io/examples/lemlist/lemlist-examples/)

#### Collections (4)

Postman and Open Collection request collections.

- [lemlist API](https://apis.io/collections/lemlist/open-lemlist/)
- [lemlist Campaigns API](https://apis.io/collections/lemlist/open-lemlist-campaigns-api/)
- [lemlist Campaigns Team API](https://apis.io/collections/lemlist/open-lemlist-team-api/)
- [lemlist Campaigns Users API](https://apis.io/collections/lemlist/open-lemlist-users-api/)

#### Overlays (22)

OpenAPI overlays, including conversational phrasing for each operation.

- [Lemlist Activities Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-activities-api-phrasing-overlay/)
- [Lemlist Api Overlay](https://apis.io/overlays/lemlist/lemlist-api-overlay/)
- [Lemlist Campaigns Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-campaigns-api-phrasing-overlay/)
- [Lemlist Companies Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-companies-api-phrasing-overlay/)
- [Lemlist Contacts Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-contacts-api-phrasing-overlay/)
- [Lemlist Deliverability Alerts Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-deliverability-alerts-api-phrasing-overlay/)
- [Lemlist Email Accounts Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-email-accounts-api-phrasing-overlay/)
- [Lemlist Enrich Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-enrich-api-phrasing-overlay/)
- [Lemlist Fields Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-fields-api-phrasing-overlay/)
- [Lemlist Inbox Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-inbox-api-phrasing-overlay/)
- [Lemlist Leads Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-leads-api-phrasing-overlay/)
- [Lemlist Lemwarm Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-lemwarm-api-phrasing-overlay/)
- [Lemlist People Database Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-people-database-api-phrasing-overlay/)
- [Lemlist Schedules Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-schedules-api-phrasing-overlay/)
- [Lemlist Sequences Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-sequences-api-phrasing-overlay/)
- [Lemlist Signal Agents Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-signal-agents-api-phrasing-overlay/)
- [Lemlist Stats Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-stats-api-phrasing-overlay/)
- [Lemlist Tasks Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-tasks-api-phrasing-overlay/)
- [Lemlist Team Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-team-api-phrasing-overlay/)
- [Lemlist Unsubscribes Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-unsubscribes-api-phrasing-overlay/)
- [Lemlist Users Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-users-api-phrasing-overlay/)
- [Lemlist Webhooks Api Phrasing Overlay](https://apis.io/overlays/lemlist/lemlist-webhooks-api-phrasing-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Lemlist Authentication](https://apis.io/security/lemlist/lemlist-authentication/)
- [Lemlist Domain Security](https://apis.io/security/lemlist/lemlist-domain-security/)
- [Lemlist Trust Center](https://apis.io/security/lemlist/lemlist-trust-center/)
- [Lemlist Vulnerability Disclosure](https://apis.io/security/lemlist/lemlist-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Lemlist Scopes](https://apis.io/scopes/lemlist/lemlist-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Lemlist Plans Pricing](https://apis.io/plans/lemlist/lemlist-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Lemlist Rate Limits](https://apis.io/rate-limits/lemlist/lemlist-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.lemlist.com)
- [Documentation](https://developer.lemlist.com)
- [Getting started](https://developer.lemlist.com/api-reference/getting-started/overview)
- [API reference](https://developer.lemlist.com/api-reference/getting-started/overview)
- [Pricing](https://www.lemlist.com/pricing)
- [Sign up](https://app.lemlist.com/create-account)
- [Support](https://help.lemlist.com)
- [Blog](https://www.lemlist.com/blog)
- [Security](https://hackerone.com/lemlist)
- [Compliance](https://trust.lemlist.com/)
- [Terms of service](https://www.lemlist.com/legal/terms)
- [Privacy policy](https://www.lemlist.com/legal/privacy-policy)
- [GitHub](https://github.com/l3mpire)
- [Status](https://status.lemlist.com)

## API Evangelist rating

**Kin Score 72.8** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 55.9 |
| Contract governance | 18.2 |
| Operational transparency | 57.9 |
| Developer ergonomics | 78.6 |
| Access clarity | 85.5 |

**Agent readiness 65.0** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/lemlist/](https://apis.io/providers/lemlist/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for lemlist: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/lemlist/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
