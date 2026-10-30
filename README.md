# Mailosaur

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

Mailosaur is an email and SMS testing platform for developers and QA teams. It provides a REST API for creating test inboxes, capturing and retrieving messages, running assertions, performing deliverability analysis, and integrating email and SMS testing into CI/CD pipelines. The platform supports authentication testing (TOTP/2FA), spam analysis, SPF/DKIM/DMARC validation, and connects via SMTP, POP3, and IMAP protocols.

**Areas:** Email Testing · SMS Testing · Developer Tools · QA Automation · CI/CD · SMTP · TOTP · Deliverability

## Mailosaur on APIs.io

Everything profiled for Mailosaur is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/mailosaur/](https://apis.io/providers/mailosaur/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Mailosaur Analysis API](https://apis.io/apis/mailosaur/mailosaur-analysis-api/) — Operations for analyzing the content and deliverability of an email, including SpamAssassin scoring and per-provider deliverability reports.
- [Mailosaur Devices API](https://apis.io/apis/mailosaur/mailosaur-devices-api/) — Operations for managing virtual security devices and retrieving their current one-time passwords (OTPs), used to automate testing of app-based multi-factor…
- [Mailosaur Files API](https://apis.io/apis/mailosaur/mailosaur-files-api/) — Operations for downloading the raw content associated with a message — file attachments, the full EML source of an email, and rendered email previews.
- [Mailosaur Messages API](https://apis.io/apis/mailosaur/mailosaur-messages-api/) — Operations for finding, retrieving, creating, forwarding, replying to, and deleting the email and SMS messages received by your Mailosaur inboxes.
- [Mailosaur Previews API](https://apis.io/apis/mailosaur/mailosaur-previews-api/) — Operations for discovering the email clients available for generating email previews (screenshots of an email rendered in real clients).
- [Mailosaur Servers API](https://apis.io/apis/mailosaur/mailosaur-servers-api/) — Operations for creating and managing your Mailosaur inboxes (servers). Inboxes group your tests together, each with its own domain and SMTP/POP3/IMAP…
- [Mailosaur Usage API](https://apis.io/apis/mailosaur/mailosaur-usage-api/) — Operations for inspecting your account's usage limits and recent transactional usage. These endpoints require authentication with an account-level API key.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [mailosaur](https://apis.io/servers/mailosaur/mailosaur/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Mailosaur Agentic Access](https://apis.io/agentic-access/mailosaur/mailosaur-agentic-access/)

#### JSON Schema (3)

The data models the API reads and writes.

- [Device](https://apis.io/schemas/mailosaur/mailosaur-device/)
- [Message](https://apis.io/schemas/mailosaur/mailosaur-message/)
- [Server](https://apis.io/schemas/mailosaur/mailosaur-server/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Mailosaur Context](https://apis.io/jsonld/mailosaur/mailosaur-context/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Mailosaur Vocabulary](https://apis.io/vocabularies/mailosaur/mailosaur-vocabulary/)

#### Examples (4)

Example requests and responses.

- [Mailosaur Create Server Example](https://apis.io/examples/mailosaur/mailosaur-create-server-example/)
- [Mailosaur Deliverability Report Example](https://apis.io/examples/mailosaur/mailosaur-deliverability-report-example/)
- [Mailosaur Get Otp Example](https://apis.io/examples/mailosaur/mailosaur-get-otp-example/)
- [Mailosaur Search Messages Example](https://apis.io/examples/mailosaur/mailosaur-search-messages-example/)

#### Collections (6)

Postman and Open Collection request collections.

- [Mailosaur Analysis API](https://apis.io/collections/mailosaur/open-mailosaur-analysis-api/)
- [Mailosaur Analysis Devices API](https://apis.io/collections/mailosaur/open-mailosaur-devices-api/)
- [Mailosaur Analysis Files API](https://apis.io/collections/mailosaur/open-mailosaur-files-api/)
- [Mailosaur Analysis Messages API](https://apis.io/collections/mailosaur/open-mailosaur-messages-api/)
- [Mailosaur Analysis Servers API](https://apis.io/collections/mailosaur/open-mailosaur-servers-api/)
- [Mailosaur Analysis Usage API](https://apis.io/collections/mailosaur/open-mailosaur-usage-api/)

#### Overlays (14)

OpenAPI overlays, including conversational phrasing for each operation.

- [Mailosaur Analysis Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-analysis-api-overlay/)
- [Mailosaur Analysis Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-analysis-api-phrasing-overlay/)
- [Mailosaur Devices Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-devices-api-overlay/)
- [Mailosaur Devices Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-devices-api-phrasing-overlay/)
- [Mailosaur Files Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-files-api-overlay/)
- [Mailosaur Files Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-files-api-phrasing-overlay/)
- [Mailosaur Messages Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-messages-api-overlay/)
- [Mailosaur Messages Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-messages-api-phrasing-overlay/)
- [Mailosaur Previews Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-previews-api-overlay/)
- [Mailosaur Previews Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-previews-api-phrasing-overlay/)
- [Mailosaur Servers Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-servers-api-overlay/)
- [Mailosaur Servers Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-servers-api-phrasing-overlay/)
- [Mailosaur Usage Api Overlay](https://apis.io/overlays/mailosaur/mailosaur-usage-api-overlay/)
- [Mailosaur Usage Api Phrasing Overlay](https://apis.io/overlays/mailosaur/mailosaur-usage-api-phrasing-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Mailosaur — jsonschema rules](https://apis.io/rules/mailosaur/mailosaur-jsonschema-spectral-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Mailosaur Authentication](https://apis.io/security/mailosaur/mailosaur-authentication/)
- [Mailosaur Domain Security](https://apis.io/security/mailosaur/mailosaur-domain-security/)
- [Mailosaur Trust Center](https://apis.io/security/mailosaur/mailosaur-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Mailosaur Plans Pricing](https://apis.io/plans/mailosaur/mailosaur-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Mailosaur Rate Limits](https://apis.io/rate-limits/mailosaur/mailosaur-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Mailosaur Finops](https://apis.io/finops/mailosaur/mailosaur-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://mailosaur.com)
- [Documentation](https://mailosaur.com/docs)
- [Getting started](https://mailosaur.com/docs/email-testing/sending-to-mailosaur)
- [API reference](https://mailosaur.com/docs/api)
- [Pricing](https://mailosaur.com/pricing)
- [Sign up](https://mailosaur.com/app/signup)
- [Support](https://mailosaur.com/contact)
- [Blog](https://mailosaur.com/blog)
- [Compliance](https://trust.mailosaur.com)
- [Terms of service](https://mailosaur.com/terms)
- [Privacy policy](https://mailosaur.com/privacy)
- [Status](https://status.mailosaur.com)

## API Evangelist rating

**Kin Score 67.7** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 59.1 |
| Contract governance | 31.8 |
| Operational transparency | 52.6 |
| Developer ergonomics | 75.6 |
| Access clarity | 92.1 |

**Agent readiness 25.5** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/mailosaur/](https://apis.io/providers/mailosaur/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Mailosaur: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/mailosaur/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
