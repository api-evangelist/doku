---
name: Bind an e-wallet and charge host-to-host
description: Bind an Indonesian e-wallet (OVO/DANA/ShopeePay/DOKU Wallet), debit host-to-host, and refund via SNAP Direct Debit.
api: openapi/doku-openapi.yml
operations: [getAccessTokenB2B, bindEwalletAccount, ewalletBalanceInquiry, debitPaymentHostToHost, debitRefund, unbindEwalletAccount]
auth: SNAP (SHA256withRSA token, then HMAC-SHA512 per transaction, Bearer token)
---

# Bind an e-wallet and charge host-to-host

Charge a bound e-wallet directly (no hosted page) via SNAP Direct Debit.

## Auth (SNAP)
Mint a Bearer token with **`getAccessTokenB2B`** (or `getAccessTokenB2B2C` for
customer-context flows), then sign each transaction with HMAC-SHA512
`X-SIGNATURE` + `X-PARTNER-ID` + `X-TIMESTAMP` + unique **`X-EXTERNAL-ID`**.

## Steps
1. **`bindEwalletAccount`** — `POST /direct-debit/core/v1/registration-account-binding`.
   Send `phoneNo`, `redirectUrl`, and `additionalInfo.channel`
   (e.g. `DIRECT_DEBIT_OVO_SNAP`). Buyer authorizes; you get a binding reference.
2. (optional) **`ewalletBalanceInquiry`** — `POST /direct-debit/core/v1/balance-inquiry`.
3. **`debitPaymentHostToHost`** — `POST /direct-debit/core/v1/debit/payment-host-to-host`.
   Send `partnerReferenceNo`, `amount` (`{value,currency:"IDR"}`),
   `additionalInfo.channel` (e.g. `EMONEY_OVO_SNAP`).
4. **`debitRefund`** — `POST /direct-debit/core/v1/debit/refund` to reverse.
5. **`unbindEwalletAccount`** — `POST /direct-debit/core/v1/registration-account-unbinding`.

## Rules
- `partnerReferenceNo` + `X-EXTERNAL-ID` are your idempotency handles — keep them
  unique per charge; retry with the same values.
- Common declines: insufficient balance, binding-not-found, user-cancelled — see
  `errors/doku-decline-codes.yml`. Reconcile against the webhook
  (`asyncapi/doku-webhooks.yml`).
