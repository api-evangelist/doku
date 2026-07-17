---
name: Disburse funds with Kirim payout
description: Check balance, validate a beneficiary bank account, transfer funds, and confirm status with Kirim DOKU.
api: openapi/doku-openapi.yml
operations: [getAccessTokenB2B, payoutBalanceInquiry, payoutAccountInquiry, payoutTransferBank, payoutCheckStatus]
auth: SNAP B2B Bearer token
---

# Disburse funds with Kirim payout

Pay out to recipient bank accounts (domestic disbursement / remittance) with the Kirim DOKU product.

## Auth (SNAP)
Mint a Bearer token with **`getAccessTokenB2B`** and send it on every Kirim call
with `X-PARTNER-ID`, `X-TIMESTAMP`, and a unique **`X-EXTERNAL-ID`**.

## Steps
1. **`payoutBalanceInquiry`** — `POST /payout/kirim-doku/balance-inquiry`. Confirm
   sufficient DOKU balance before disbursing.
2. **`payoutAccountInquiry`** — `POST /payout/kirim-doku/account-inquiry`. Validate
   the beneficiary account number + bank code and read back the account name.
3. **`payoutTransferBank`** — `POST /payout/kirim-doku/transfer-bank`. Send
   `partnerReferenceNo`, beneficiary details, and `amount` (`{value,currency:"IDR"}`).
4. **`payoutCheckStatus`** — `POST /payout/kirim-doku/check-status`. Poll until the
   disbursement reaches a terminal state.

## Rules
- **Always** run `payoutAccountInquiry` before `payoutTransferBank` — a wrong
  account is unrecoverable.
- `partnerReferenceNo` + `X-EXTERNAL-ID` are the idempotency handles; a duplicate
  reference is rejected. Insufficient balance and account-not-found are the
  common rejections — see `errors/doku-decline-codes.yml`.
