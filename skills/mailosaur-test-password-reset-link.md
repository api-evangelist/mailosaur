---
name: Test a password-reset or account-verification link end to end
description: >-
  Capture the transactional email your product sends, pull the reset or
  verification hyperlink out of the parsed body, and follow it — the standard
  end-to-end flow behind "click the link in your email".
api: openapi/mailosaur-messages-api-openapi.yml
operations: [listServers, searchMessages, getMessage, getEmailFile, deleteMessage]
generated: '2026-08-14'
method: generated
source: >-
  openapi/mailosaur-messages-api-openapi.yml and
  openapi/mailosaur-files-api-openapi.yml (operationIds verified verbatim),
  conventions/mailosaur-conventions.yml, https://mailosaur.com/docs/automation/links
---

# Test a password-reset or account-verification link end to end

## Before you start

- Base URL `https://mailosaur.com/api`, HTTP Basic auth, API key as the
  username with an empty password.
- Have an inbox (server) id — `listServers` returns `items[].id`.

## Steps

1. **Record the cutoff timestamp**, then request the password reset in your
   product for an address at the inbox's domain.

2. **Wait for the email.**
   `POST /api/messages/search?server={serverId}&timeout=20000&receivedAfter={cutoff}`
   with `SearchCriteria` — `sentTo` set to the address, and `subject` if several
   message types can arrive.

3. **Retrieve the full message.** `GET /api/messages/{messageId}` using
   `items[0].id`. Search results are summaries and contain no body.

4. **Take the link from the parsed content, not from a regex.**
   `html.links[]` gives `{href, text}` for every hyperlink Mailosaur found;
   `text.links[]` does the same for the plain-text part. Select by `text`
   (the anchor label, e.g. "Reset your password") rather than by position —
   position changes whenever marketing edits the template.

5. **Follow the `href`** with your HTTP client or browser driver and assert the
   product lands on the reset page and accepts a new password.

6. **Assert the rest of the email while you have it.** `subject`, `from[]`,
   `to[]`, `received`, `attachments[]`, and `metadata.headers[]` for header
   assertions (`metadata.ehlo`, `metadata.mailFrom`, `metadata.rcptTo` carry
   the SMTP envelope).

7. **Need the raw source?** `GET /api/files/email/{messageId}` (`getEmailFile`)
   downloads the full EML. Use it for MIME-structure assertions the parsed
   model does not expose.

8. **Clean up** with `deleteMessage` — permanent, no undo.

## Rules that will bite you

- **`html.links` includes tracking and unsubscribe URLs.** Match on the anchor
  text or on a URL prefix you control; never take `links[0]`.
- **Web beacons appear in `html.images`**, not in `links` — check there if you
  are asserting open-tracking pixels.
- **Timing out is a 200 with `items: []`.** Assert on the array, not the status.
- **No idempotency key exists.** Do not blind-retry the trigger step; you will
  generate a second email and may assert against the stale one. Always scope
  with `receivedAfter`.
