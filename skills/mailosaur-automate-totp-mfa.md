---
name: Automate authenticator-app (TOTP) multi-factor login
description: >-
  Generate the current 6-digit TOTP code for an authenticator-app enrolment, so
  a test or an agent can get past an MFA challenge that would otherwise need a
  phone in someone's hand.
api: openapi/mailosaur-devices-api-openapi.yml
operations: [getOtpBySharedSecret, createDevice, listDevices, getDeviceOtp, deleteDevice]
generated: '2026-08-14'
method: generated
source: >-
  openapi/mailosaur-devices-api-openapi.yml (operationIds verified verbatim),
  https://mailosaur.com/docs/authenticator/automate-totp-testing,
  https://mailosaur.com/docs/authenticator/create-and-delete-devices
---

# Automate authenticator-app (TOTP) multi-factor login

Mailosaur's virtual authenticator behaves like Google Authenticator: give it the
shared secret your product issued at enrolment, and it returns the current code.

## Before you start

- Base URL `https://mailosaur.com/api`, HTTP Basic auth with the API key as the
  username and an empty password.
- Devices are **account-level**, not scoped to an inbox — unlike every message
  operation, no `server` parameter is involved.
- You need the TOTP shared secret. Your product surfaces it during enrolment,
  usually as the `secret` parameter inside the `otpauth://` QR code URI.

## Choose one of two paths

### Path A — stateless, no device stored

Use when the secret is available in the test at the moment you need a code.

1. `POST /api/devices/otp` (`getOtpBySharedSecret`) with the shared secret in
   the request body.
2. Read `code` from the response and submit it to the MFA challenge.

Nothing is persisted, so there is nothing to clean up. Prefer this path for
ephemeral test users.

### Path B — stored device, reusable

Use when the same enrolment is exercised across many runs.

1. `POST /api/devices` (`createDevice`) with a name and the shared secret. Keep
   the returned device `id`.
2. `GET /api/devices/{deviceId}/otp` (`getDeviceOtp`) whenever you need the
   current code.
3. `GET /api/devices` (`listDevices`) to find an existing device id.
4. `DELETE /api/devices/{deviceId}` (`deleteDevice`) when the enrolment is
   retired.

## Rules that will bite you

- **Codes rotate on the standard 30-second TOTP window.** Fetch the code
  immediately before submitting it. If your form fill takes longer than the
  remaining window, fetch again rather than reusing.
- **The shared secret is a credential.** Never write it into a repository, a
  fixture file, or a log line. Pass it from your secret store.
- **`createDevice` is not idempotent.** Calling it twice with the same secret
  creates two devices. Call `listDevices` first if you intend the device to be
  singular.
- **Errors are thin.** A wrong or malformed secret returns 400 with the
  `{type, message, parameters, model}` envelope; 401 and 404 return no body at
  all.
- **This flow needs a standard (account-wide) API key.** A server-restricted key
  is scoped to one inbox and cannot manage account-level devices.
