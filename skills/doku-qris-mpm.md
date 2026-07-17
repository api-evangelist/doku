---
name: Generate and reconcile a QRIS payment
description: Generate a QRIS Merchant-Presented Mode code, query its status, and refund via SNAP.
api: openapi/doku-openapi.yml
operations: [getAccessTokenB2B, generateQrisMpm, queryQrisMpm, refundQrisMpm]
auth: SNAP (SHA256withRSA token, then HMAC-SHA512 per transaction, Bearer token)
---

# Generate and reconcile a QRIS payment

QRIS is Bank Indonesia's unified national QR standard; any QRIS wallet/bank app can pay a Merchant-Presented QR.

## Auth (SNAP)
Mint a Bearer token with **`getAccessTokenB2B`**, then sign each request with
HMAC-SHA512 `X-SIGNATURE` + `X-PARTNER-ID` + `X-TIMESTAMP` + unique
**`X-EXTERNAL-ID`**.

## Steps
1. **`generateQrisMpm`** — `POST /snap-adapter/b2b/v1.0/qr/qr-mpm-generate`.
   Send `partnerReferenceNo`, `amount` (`{value,currency:"IDR"}`), `merchantId`,
   `validityPeriod`. Response returns the QR string/image to display.
2. Buyer scans and pays. Receive the result on your payment notification URL
   (`asyncapi/doku-webhooks.yml`).
3. **`queryQrisMpm`** — `POST /snap-adapter/b2b/v1.0/qr/qr-mpm-query` to confirm
   status if the webhook is delayed.
4. **`refundQrisMpm`** — `POST /snap-adapter/b2b/v1.0/qr/qr-mpm-refund` to reverse.

## Rules
- Set a sensible `validityPeriod`; expired QRs must be regenerated.
- Idempotency via unique **`X-EXTERNAL-ID`** / `partnerReferenceNo`.
- Success `responseCode 2002700`; see `errors/doku-problem-types.yml`.
