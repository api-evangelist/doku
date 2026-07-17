# DOKU (doku)

DOKU (PT Nusa Satu Inti Artha) is Indonesia's pioneering payment gateway, founded in 2007 and licensed by Bank Indonesia as a Category 1 Payment Service Provider. Its developer platform exposes a hosted Checkout API plus a full suite of Bank Indonesia SNAP (Standar Nasional Open API Pembayaran) endpoints for Virtual Account, e-Wallet, Direct Debit, QRIS, and Kirim (payout/disbursement), all settling in Indonesian Rupiah (IDR).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/doku/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/doku/refs/heads/main/apis.yml)

## Tags

- Payments
- Payment Gateway
- Fintech
- Indonesia
- SEA
- SNAP
- Virtual Account
- E-Wallet
- QRIS
- Direct Debit
- Payouts

## Timestamps

- **Created:** 2026-07-17
- **Modified:** 2026-07-17

## APIs

### DOKU Checkout API

DOKU's hosted checkout page. A single `POST /checkout/v1/payment` call returns a redirect URL and token for a DOKU-hosted payment page that accepts cards, virtual accounts, e-wallets, and QRIS. Uses non-SNAP Client-Id + Request-Id + Request-Timestamp + HMAC-SHA256 Signature headers.

- **Human URL:** [https://developers.doku.com/accept-payments/doku-checkout](https://developers.doku.com/accept-payments/doku-checkout)
- **Base URL:** `https://api.doku.com`

#### Tags

- Checkout
- Hosted Payment Page
- Payments

#### Properties

- [Documentation](https://developers.doku.com/accept-payments/doku-checkout)
- [API Reference](https://developers.doku.com/accept-payments/doku-checkout/integration-guide/backend-integration)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### DOKU SNAP Access Token API

Bank Indonesia SNAP B2B and B2B2C access-token endpoints. Merchants sign an asymmetric SHA256withRSA request with X-CLIENT-KEY + X-TIMESTAMP to mint a 15-minute Bearer token used across all SNAP transaction APIs.

- **Human URL:** [https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/get-token-api/b2b](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/get-token-api/b2b)
- **Base URL:** `https://api.doku.com`

#### Tags

- Authentication
- OAuth
- SNAP

#### Properties

- [Documentation](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/get-token-api/b2b)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### DOKU SNAP Virtual Account API

SNAP BI-SNAP Virtual Account create/update/delete/inquiry across BCA, BRI, BNI, Mandiri, Permata, BTN, Danamon and other banks. HMAC-SHA512 signed transactions under `/virtual-accounts/bi-snap-va/v1.1/transfer-va`.

- **Human URL:** [https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/virtual-account/bca-virtual-account](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/virtual-account/bca-virtual-account)
- **Base URL:** `https://api.doku.com`

#### Tags

- Virtual Account
- Bank Transfer
- SNAP

#### Properties

- [Documentation](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/virtual-account/bca-virtual-account)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### DOKU SNAP Direct Debit & e-Wallet API

SNAP account-binding, host-to-host debit, refund, and unbinding for Indonesian e-wallets (OVO, DANA, ShopeePay, DOKU Wallet) and bank direct debit, under `/direct-debit/core/v1`.

- **Human URL:** [https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/e-wallet/ovo](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/e-wallet/ovo)
- **Base URL:** `https://api.doku.com`

#### Tags

- E-Wallet
- Direct Debit
- OVO
- DANA
- ShopeePay
- SNAP

#### Properties

- [Documentation](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/e-wallet/ovo)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### DOKU SNAP QRIS API

SNAP QRIS Merchant-Presented Mode (MPM) generate, query, decode, refund, and expire, plus B2B2C QR payment, under `/snap-adapter/b2b/v1.0/qr`. QRIS is Bank Indonesia's unified national QR payment standard.

- **Human URL:** [https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/qris](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/qris)
- **Base URL:** `https://api.doku.com`

#### Tags

- QRIS
- QR Code
- SNAP

#### Properties

- [Documentation](https://developers.doku.com/accept-payments/direct-api/snap/integration-guide/qris)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### DOKU Kirim Payout API

Kirim DOKU domestic disbursement — balance inquiry, bank-account inquiry, bank transfer, and transaction status — for paying out to recipient bank accounts. Authenticated with the SNAP B2B Bearer token.

- **Human URL:** [https://developers.doku.com/payout/kirim-doku](https://developers.doku.com/payout/kirim-doku)
- **Base URL:** `https://api.doku.com`

#### Tags

- Payout
- Disbursement
- Remittance
- SNAP

#### Properties

- [Documentation](https://developers.doku.com/payout/kirim-doku)
- [OpenAPI](openapi/doku-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/doku.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

## Common Properties

- [GitHub Organization](https://github.com/PTNUSASATUINTIARTHA-DOKU)
- [Website](https://www.doku.com/)
- [Documentation](https://developers.doku.com/)
- [Plans](plans/doku-plans-pricing.yml)
- [Rate Limits](rate-limits/doku-rate-limits.yml)
- [Fin Ops](finops/doku-finops.yml)
- [Authentication](authentication/doku-authentication.yml)
- [Domain Security](security/doku-domain-security.yml)
- [Trust Center](security/doku-trust-center.yml)
- [Vulnerability Disclosure](security/doku-vulnerability-disclosure.yml)
- [Agentic Access](agentic-access/doku-agentic-access.yml)
- [Blog](https://www.doku.com/en-us/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
