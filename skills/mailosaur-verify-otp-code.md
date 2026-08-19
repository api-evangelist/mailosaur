---
name: Verify a one-time passcode delivered by email or SMS
description: >-
  Capture the signup/login message your product sends to a Mailosaur inbox and
  read the verification code out of it, so an automated test or an agent can
  complete the flow without a human.
api: openapi/mailosaur-messages-api-openapi.yml
operations: [listServers, searchMessages, getMessage]
generated: '2026-08-14'
method: generated
source: >-
  openapi/mailosaur-messages-api-openapi.yml (operationIds verified verbatim),
  conventions/mailosaur-conventions.yml, errors/mailosaur-problem-types.yml,
  https://mailosaur.com/docs/automation/codes
---

# Verify a one-time passcode delivered by email or SMS

## Before you start

- Base URL is `https://mailosaur.com/api`. HTTPS only — plain HTTP fails.
- Authenticate with HTTP Basic: API key as the username, empty password
  (`-u api:YOUR_API_KEY`). A **server-restricted** key reaches exactly one
  inbox; a **standard** key reaches all of them.
- You need an inbox (server) id. Call `listServers` and take `items[].id`, or
  use the id you already hold.
- Every Mailosaur inbox accepts unlimited addresses at its own domain, so use a
  fresh address per test run rather than reusing one.

## Steps

1. **Note the cutoff time before you trigger anything.** Record the current
   UTC timestamp. You will pass it as `receivedAfter` so you cannot match a
   message from an earlier run.

2. **Trigger the flow in your product** (submit the signup form, request the
   code) using an address at the inbox's domain, or the inbox's test phone
   number for SMS.

3. **Wait for the message with `searchMessages`.**
   `POST /api/messages/search?server={serverId}&timeout=20000&receivedAfter={cutoff}`
   with a `SearchCriteria` body — `sentTo` (the address or phone number you
   used) plus `subject` or `body` if you need to disambiguate. Set `match` to
   `ALL` (the default) so every criterion must hold.
   The `timeout` is milliseconds and is the whole point of this operation: the
   server holds the request open until a match arrives. **Do not poll in a tight
   loop** — set the timeout instead.

4. **Fetch the full message with `getMessage`.**
   `GET /api/messages/{messageId}` using `items[0].id` from the search result.
   This step is mandatory: `searchMessages` returns `MessageSummary` objects,
   which carry no body content.

5. **Read the code.** Mailosaur extracts verification codes for you:
   `html.codes[].value` for an HTML email, `text.codes[].value` for plain text
   or SMS. Prefer these over regexing `html.body` yourself.

6. **Clean up** if the test owns the message: `deleteMessage`
   (`DELETE /api/messages/{messageId}`), or `deleteAllMessages`
   (`DELETE /api/messages?server={serverId}`) at the end of a suite. Both are
   permanent and cannot be undone.

## Rules that will bite you

- **A search that times out returns 200 with an empty `items` array**, not an
  error. Assert on `items.length`, never on the status code alone.
- **Retries are not safe.** Mailosaur documents no idempotency key. Nothing
  here is destructive except step 6, but if your flow re-triggers the send you
  will produce a second message and may match the wrong one — which is exactly
  why step 1 exists.
- **Errors carry almost nothing.** 401 and 404 return an empty body; only 400
  returns the `{type, message, parameters, model}` envelope. A 404 on
  `getMessage` may mean the message is outside a server-restricted key's scope
  rather than absent.
- **The daily email allowance is enforced at the mail layer.** Over-limit
  inbound email is rejected and over-limit inbound SMS is silently dropped, with
  no HTTP signal to the caller. If messages stop arriving for no visible reason,
  call `getUsageLimits` before debugging your product.
