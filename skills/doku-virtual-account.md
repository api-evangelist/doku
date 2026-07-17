---
name: Issue and reconcile a SNAP Virtual Account
description: Mint a SNAP access token, create a Bank Indonesia SNAP Virtual Account, and reconcile payment by inquiry + webhook.
api: openapi/doku-openapi.yml
operations: [getAccessTokenB2B, createVirtualAccount, inquiryVirtualAccountStatus, deleteVirtualAccount]
auth: SNAP (SHA256withRSA token, then HMAC-SHA512 per transaction, Bearer token)
---

# Issue and reconcile a SNAP Virtual Account

Create a bank Virtual Account number (BCA, BRI, BNI, Mandiri, Permata, BTN, Danamon, …) the buyer pays by transfer.

## Auth (SNAP)
1. **`getAccessTokenB2B`** — `POST /authorization/v1/access-token/b2b`. Sign
   `clientId|X-TIMESTAMP` with SHA256withRSA (`X-SIGNATURE`), send `X-CLIENT-KEY`
   + `X-TIMESTAMP`. Receive a ~15-minute Bearer `accessToken`.
2. On every transaction below, add the Bearer token plus an HMAC-SHA512
   `X-SIGNATURE`, `X-PARTNER-ID`, `X-TIMESTAMP`, and a unique **`X-EXTERNAL-ID`**
   (idempotency key). See `conventions/doku-conventions.yml`.

## Steps
1. **`createVirtualAccount`** — `POST /virtual-accounts/bi-snap-va/v1.1/transfer-va/create-va`.
   Send `partnerServiceId`, `customerNo`, `virtualAccountNo`, `virtualAccountName`,
   `trxId`, `totalAmount` (`{value,currency:"IDR"}`), and optional
   `virtualAccountConfig.reusableStatus`.
2. Buyer transfers to the VA. Receive the async result on your payment
   notification URL (`asyncapi/doku-webhooks.yml`).
3. **`inquiryVirtualAccountStatus`** — `POST /virtual-accounts/bi-snap-va/v1.1/transfer-va/inquiry`
   to confirm status if the webhook is delayed.
4. **`deleteVirtualAccount`** — `DELETE .../delete-va` to cancel an unpaid VA.

## Rules
- Reuse the same **`X-EXTERNAL-ID`** on retries to stay idempotent; a new payload
  under a used id returns a `409` conflict.
- Success is `responseCode 2002700`; not-found `4042712`, already-paid `4042714`,
  invalid amount `4042719` — see `errors/doku-decline-codes.yml`.
- Amounts are decimal strings in **IDR** (e.g. `"50000.00"`).
