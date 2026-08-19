---
name: Provision and tear down a disposable test inbox
description: >-
  Create an isolated Mailosaur inbox for a test run or an agent session, read its
  SMTP/POP3/IMAP credentials, and delete it cleanly afterwards — the setup and
  teardown every other Mailosaur flow depends on.
api: openapi/mailosaur-servers-api-openapi.yml
operations: [listServers, createServer, getServer, updateServer, getServerPassword, deleteServer, deleteAllMessages, getUsageLimits]
generated: '2026-08-14'
method: generated
source: >-
  openapi/mailosaur-servers-api-openapi.yml, openapi/mailosaur-messages-api-openapi.yml
  and openapi/mailosaur-usage-api-openapi.yml (operationIds verified verbatim),
  https://mailosaur.com/docs/inboxes, https://mailosaur.com/docs/inboxes/smtp-pop3-imap
---

# Provision and tear down a disposable test inbox

In the API an inbox is called a **server**. It is the container for everything:
its own domain, its own message store, its own SMTP/POP3/IMAP credentials.

## Before you start

- Base URL `https://mailosaur.com/api`, HTTP Basic auth with the API key as the
  username and an empty password.
- **This flow requires a standard (account-wide) API key.** A server-restricted
  key is scoped to one inbox and cannot create or delete inboxes.

## Steps

1. **Check what already exists.** `GET /api/servers` (`listServers`) returns
   `items[]` of `{id, name, users, messages}`, alphabetically. Reuse before you
   create — inbox count is a hard account quota, not a metered allowance.

2. **Create the inbox.** `POST /api/servers` (`createServer`) with a
   `ServerCreateOptions` body — just `name`. Keep the returned `id`; every
   message operation takes it as the required `server` query parameter.

3. **Address it.** Every address at the inbox's domain routes to it, and there is
   no limit on how many you use. Generate a fresh local part per test
   (`run-<uuid>@<inbox-domain>`) instead of sharing one address across runs.

4. **Get protocol credentials if you need them.**
   `GET /api/servers/{serverId}/password` (`getServerPassword`) returns the
   password used for SMTP, POP3 and IMAP. SMTP is available on every plan; POP3
   and IMAP require Core or Enterprise. Treat the value as a secret — never log
   it, never commit it.

5. **Rename or reconfigure** with `PUT /api/servers/{serverId}`
   (`updateServer`); read current state with `GET /api/servers/{serverId}`
   (`getServer`).

6. **Tear down.** Two different scopes, pick deliberately:
   - `DELETE /api/messages?server={serverId}` (`deleteAllMessages`) — empties
     the inbox, keeps it.
   - `DELETE /api/servers/{serverId}` (`deleteServer`) — deletes the inbox and
     **every message and attachment in it**.
   Both are permanent and cannot be undone.

## Rules that will bite you

- **`deleteServer` is the most destructive call in the API and has no
  confirmation, no soft delete and no idempotency key.** Never run it against an
  id you did not create in the same session. Prefer `deleteAllMessages` between
  runs and reserve `deleteServer` for inboxes your process owns end to end.
- **`createServer` is not idempotent.** Re-running a failed create leaves you
  with two inboxes and burns the quota. Call `listServers` and match on `name`
  before creating.
- **Inboxes are a quota, messages are an allowance.** `getUsageLimits`
  (`GET /api/usage/limits`) returns current limits and consumption for servers,
  users, email and SMS. Read it before provisioning in a loop.
- **A 404 can mean "not yours".** With a server-restricted key, any inbox
  outside its scope is indistinguishable from one that does not exist, and the
  401/404 responses carry no body to tell you which.
