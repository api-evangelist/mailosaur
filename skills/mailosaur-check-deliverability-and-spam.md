---
name: Check an email's deliverability and spam score before it ships
description: >-
  Run SpamAssassin scoring and a full deliverability report (SPF, DKIM, DMARC,
  DNS records, blocklists, content checks) against a message your product
  actually sent, so a regression in the template or the sending domain fails the
  build instead of the campaign.
api: openapi/mailosaur-analysis-api-openapi.yml
operations: [searchMessages, getSpamAnalysis, getDeliverabilityReport]
generated: '2026-08-14'
method: generated
source: >-
  openapi/mailosaur-analysis-api-openapi.yml and
  openapi/mailosaur-messages-api-openapi.yml (operationIds verified verbatim),
  https://mailosaur.com/docs/email-testing/deliverability,
  https://mailosaur.com/docs/automation/spam
---

# Check an email's deliverability and spam score before it ships

## Before you start

- Base URL `https://mailosaur.com/api`, HTTP Basic auth, API key as username,
  empty password.
- Both analyses run against a message Mailosaur has **already captured**. You
  cannot analyse a template — send it to an inbox first.

## Steps

1. **Send the email from your product** to an address at the inbox's domain.

2. **Capture it.**
   `POST /api/messages/search?server={serverId}&timeout=20000&receivedAfter={cutoff}`
   with `SearchCriteria` (`sentTo`, and `subject` when several templates land in
   the same inbox). Take `items[0].id`.

3. **Score it for spam.** `GET /api/analysis/spam/{messageId}`
   (`getSpamAnalysis`) returns a `SpamAnalysisResult` — the SpamAssassin total
   plus every `SpamAssassinRule` that fired, with its individual score. Assert
   on the total against a threshold you own, and log the rule list so a
   regression names itself.

4. **Run the full deliverability report.**
   `GET /api/analysis/deliverability/{messageId}` (`getDeliverabilityReport`)
   returns a `DeliverabilityReport` covering:
   - `EmailAuthenticationResult` for **SPF, DKIM and DMARC**
   - `DnsRecords` — checks against the sending domain
   - `BlockListResult` — one entry per blocklist checked
   - `Content` — content checks on the email itself
   - `SpamFilterResults` — spam-filter analysis

5. **Fail the build on what you care about.** Authentication failures (SPF/DKIM/
   DMARC) and blocklist hits are infrastructure regressions and should block a
   release; content and spam-score drift is usually a template review.

## Rules that will bite you

- **These report on the message as received by Mailosaur**, which means they
  measure your sending configuration for *that* path. A pass here is not a
  guarantee at every inbox provider.
- **Both operations are read-only GETs and safe to retry.** They are the only
  part of this flow that is.
- **Analysis needs the message id, not the summary.** Search returns summaries;
  `items[].id` is what these paths take.
- **Nothing is versioned.** The report shape can change without a version bump —
  the API carries no version segment, header or date pin. Assert on the fields
  you need rather than deep-equal on the whole document.
