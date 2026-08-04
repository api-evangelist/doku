# DOKU (doku)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
