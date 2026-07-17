---
name: Create a DOKU-hosted checkout page
description: Generate a DOKU-hosted payment page (accepts cards, VA, e-wallets, QRIS) and receive the result via webhook.
api: openapi/doku-openapi.yml
operations: [createCheckoutPayment]
auth: non-SNAP (Client-Id + Request-Id + Request-Timestamp + HMAC-SHA256 Signature)
---

# Create a DOKU-hosted checkout page

Use this for the fastest integration: DOKU hosts the payment UI and returns a URL you redirect the buyer to.

## Auth (non-SNAP)
This flow uses the non-SNAP header scheme, not a SNAP Bearer token. On every
request send `Client-Id`, `Request-Id`, `Request-Timestamp`, and a `Signature`
header where `Signature = "HMACSHA256=" + base64(HMAC-SHA256(clientSecret,
componentString))`. See `authentication/doku-authentication.yml`.

## Steps
1. **`createCheckoutPayment`** — `POST /checkout/v1/payment`. Send `order.amount`
   (integer, IDR), `order.invoice_number` (unique, your reference),
   `payment.payment_due_date` (minutes to expiry), and `customer`. Response
   returns `response.payment.url` (the hosted page) and `token_id`.
2. Redirect the buyer to `response.payment.url`.
3. Receive the async result on your registered **payment notification URL**
   (see `asyncapi/doku-webhooks.yml`). Verify the HMAC-SHA256 `Signature` header,
   apply a replay guard, and dedupe on `invoice_number` before fulfilling.

## Rules
- Amounts settle in **IDR**.
- `invoice_number` is your idempotency/business reference — keep it unique and
  reconcile the webhook against it. On the non-SNAP API, `Request-Id` is the
  per-request unique reference.
- Errors come back as a `message[]` array; see `errors/doku-problem-types.yml`.
- Test in the sandbox at `https://api-sandbox.doku.com` and drive the outcome
  with the Simulator (`sandbox/doku-sandbox.yml`).
