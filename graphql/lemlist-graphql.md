# lemlist GraphQL Schema

> **Not a lemlist product. Not published by lemlist.**
> lemlist ships **no** GraphQL API. Probed 2026-08-13: `POST /graphql` returned
> HTTP 405 Method Not Allowed on `api.lemlist.com`, `app.lemlist.com` and
> `api.lemlist.com/api`, and no GraphQL endpoint appears anywhere in lemlist's
> documentation, its `llms.txt`, or its published OpenAPI.
> The schema in this directory is an API Evangelist **modelling exercise** derived
> from the REST surface, retained for reference only. The `type: GraphQL` pointer
> was removed from `apis.yml` on 2026-08-13 because it asserted a surface the
> provider does not serve.

Conceptual GraphQL schema for the [lemlist](https://www.lemlist.com) sales engagement and email outreach automation platform. lemlist enables sales teams to build prospect lists, run personalized multichannel outreach across email and LinkedIn, and automate follow-up sequences. The REST API is documented at [developer.lemlist.com](https://developer.lemlist.com).

This schema is derived from the lemlist REST API surface and models the core domain objects and operations available to developers.

## Schema File

- [lemlist-schema.graphql](lemlist-schema.graphql)

## Type Coverage

The schema defines the following named types organized by domain:

### Campaign

| Type | Description |
|------|-------------|
| `Campaign` | Core campaign object with status, type, sender, and schedule |
| `CampaignDetails` | Extended campaign with steps, leads, reports, and A/B tests |
| `CampaignStatus` | Enum: DRAFT, ACTIVE, PAUSED, STOPPED, ARCHIVED |
| `CampaignType` | Enum: EMAIL, LINKEDIN, MULTICHANNEL, API |
| `CampaignStep` | A step within a campaign sequence |
| `CampaignStepType` | Enum covering email, LinkedIn, call, task, and API step types |
| `CampaignSettings` | Per-campaign configuration (reply tracking, daily limits, timezone) |

### Steps

| Type | Description |
|------|-------------|
| `Step` | Base step reference (type, order, delay) |
| `StepDetails` | Polymorphic step content (subject, body, LinkedIn message, API config) |
| `StepDelay` | Delay between steps (amount + unit) |
| `EmailStep` | Email step with subject, body, tracking, and personalization |
| `LinkedinStep` | LinkedIn visit, connect, or message step |
| `CallStep` | Manual call step with instructions |
| `ApiStep` | Outbound API/webhook step with URL, method, headers, and body |
| `Hook` | Event hook tied to a campaign step |

### Sequence

| Type | Description |
|------|-------------|
| `Sequence` | Named sequence of steps within a campaign |
| `SequenceDetails` | Extended sequence with lead count and update timestamp |
| `SequenceStep` | Individual step inside a sequence |

### Lead

| Type | Description |
|------|-------------|
| `Lead` | Core lead record with email, name, company, and status |
| `LeadDetails` | Extended lead with LinkedIn, enrichment, icebreaker, and custom fields |
| `LeadStatus` | Enum covering all lead lifecycle states |
| `LeadContact` | Contact details including phone, LinkedIn, company, and job title |
| `LeadActivity` | Individual activity record for a lead |
| `LeadEnrichment` | Enrichment data sourced from LinkedIn or third-party providers |

### Activity and Email Events

| Type | Description |
|------|-------------|
| `Activity` | Generic activity event across all channels |
| `ActivityType` | Enum covering 18 activity types across email, LinkedIn, calls, and API |
| `Email` | Sent email record with status |
| `EmailDetails` | Extended email with full event history |
| `EmailStatus` | Enum: PENDING, SENT, DELIVERED, OPENED, CLICKED, REPLIED, BOUNCED, FAILED |
| `EmailEvent` | Individual email interaction event (open, click, reply, bounce) |
| `Opened` | Email open event with IP address and open count |
| `Clicked` | Email click event with link and click count |
| `Replied` | Reply event with reply body and subject |
| `Bounce` | Bounce event with type and reason |
| `Unsubscribe` | Unsubscribe record with campaign, reason, and source |
| `Interest` | Lead marked as interested event |

### Team and Sender

| Type | Description |
|------|-------------|
| `Team` | Team object with members |
| `TeamDetails` | Extended team with plan, campaign count, and lead count |
| `Sender` | Sending account linked to a team |
| `SenderDetails` | Extended sender with LinkedIn connection, warmup, inbox, and schedules |

### Schedule and Inbox

| Type | Description |
|------|-------------|
| `Schedule` | Sending schedule (days, hours, timezone) |
| `Inbox` | Sending inbox linked to a sender with warmup and daily limit |

### List and Blacklist

| Type | Description |
|------|-------------|
| `Blacklist` | Team-level blacklist for email addresses and domains |
| `BlacklistEntry` | Individual blacklist entry |
| `List` | Named lead list |
| `ListDetails` | Extended list with members |
| `ListMember` | Individual member entry in a list |

### Personalization and Templates

| Type | Description |
|------|-------------|
| `Variable` | Custom variable attached to a lead |
| `PersonalizationTag` | Dynamic tag usable in email bodies (e.g., `{{firstName}}`) |
| `SmartLiquid` | Conditional personalization block with true/false rendering |
| `Template` | Reusable email or step template |
| `TemplateDetails` | Extended template with personalization tags, smart liquid, and usage count |

### Integrations

| Type | Description |
|------|-------------|
| `Integration` | Generic integration record |
| `IntegrationType` | Enum covering Salesforce, HubSpot, Pipedrive, Zapier, Make, and more |
| `CRM` | CRM connection with sync state |
| `CRMIntegration` | CRM integration with field mapping configuration |
| `SalesforceIntegration` | Salesforce-specific integration with object sync toggles |
| `HubSpotIntegration` | HubSpot-specific integration with portal ID and deal sync |

### Reporting and Analytics

| Type | Description |
|------|-------------|
| `Report` | Campaign-level aggregate report (sent, opened, replied, bounce rates) |
| `Metric` | Single named metric with value and period |
| `Stat` | Daily campaign stats snapshot |
| `ABTest` | A/B test on a campaign step |
| `ABTestStatus` | Enum: RUNNING, WINNER_PICKED, COMPLETED |
| `ABTestVariant` | Individual A/B test variant with performance metrics |

### Webhooks and Auth

| Type | Description |
|------|-------------|
| `Webhook` | Outbound webhook registration for campaign events |
| `WebhookEvent` | Enum of triggerable webhook events |
| `APIKey` | API key with name, prefix, and permissions |
| `Token` | Authentication token with scopes and expiry |

## Root Operations

### Query

- `campaign(id)`, `campaigns(status, type, limit, offset)` — retrieve campaigns
- `campaignReport(id)`, `campaignStats(id, startDate, endDate)` — analytics
- `campaignLeads(campaignId, status, limit, offset)` — leads in a campaign
- `lead(id)`, `leadByEmail(email)`, `leads(...)` — lead lookups
- `leadActivities(leadId, ...)` — activity history for a lead
- `sequence(id)`, `sequences(campaignId)` — sequences
- `team`, `sender(id)`, `senders` — team and sender info
- `schedule(id)`, `schedules` — sending schedules
- `inbox(senderId)` — sender inbox details
- `blacklist` — team blacklist
- `list(id)`, `lists(...)` — lead lists
- `template(id)`, `templates(...)` — templates
- `webhooks(campaignId)` — webhook registrations
- `integrations`, `salesforceIntegration`, `hubspotIntegration` — integrations
- `abTest(id)`, `abTests(campaignId)` — A/B tests
- `apiKeys` — API key management

### Mutation

- Campaign lifecycle: create, update, delete, pause, resume
- Step management: add email/LinkedIn/call/API steps, update, delete
- Lead management: add, update, delete, pause, resume, mark interested/not-interested, unsubscribe
- Blacklist: add and remove entries
- List management: create, update, delete, add/remove members
- Webhook management: create, update, delete
- Template management: create, update, delete
- Schedule management: create, update, delete
- API key management: create, delete

### Subscription

- Real-time events: `emailSent`, `emailOpened`, `emailClicked`, `emailReplied`, `emailBounced`, `leadUnsubscribed`, `leadInterested`, `activityLogged`

## Source

- REST API reference: https://developer.lemlist.com
- Provider website: https://www.lemlist.com
