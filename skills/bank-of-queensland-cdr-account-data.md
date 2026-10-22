---
name: bank-of-queensland-cdr-account-data
description: >-
  Read a consenting BOQ customer's accounts, balances and transactions through
  the Consumer Data Right (CDR) Banking APIs. Only usable by an ACCC-accredited
  Data Recipient holding a valid CDR consent (FAPI OAuth2/OIDC access token over mTLS).
api: openapi/bank-of-queensland-banking-accounts-api-openapi.yml
apis:
  - openapi/bank-of-queensland-banking-accounts-api-openapi.yml
  - openapi/bank-of-queensland-banking-account-balances-api-openapi.yml
  - openapi/bank-of-queensland-banking-account-transactions-api-openapi.yml
auth: cdr-adr-oauth2-fapi
operations:
  - listBankingAccounts
  - getBankingAccountDetail
  - listBankingBalancesBulk
  - getBankingBalance
  - listBankingTransactions
  - getBankingTransactionDetail
generated: '2026-10-20'
method: generated
---

# Read BOQ customer account data (CDR)

These operations come from the shared DSB Consumer Data Standards Banking API
v1.36.0, which BOQ implements as a CDR data holder. They are **not** open: the
caller must be an accredited Data Recipient with an active consent covering the
`bank:accounts.basic:read`, `bank:accounts.detail:read` and
`bank:transactions:read` style scopes the standard defines.

1. `listBankingAccounts`: list the consented accounts (filters: `product-category`,
   `open-status`, `is-owned`; paginate with `page` / `page-size`).
2. `getBankingAccountDetail`: pull the detail for one `accountId`.
3. `listBankingBalancesBulk` (or `getBankingBalance` per `accountId`): read balances.
4. `listBankingTransactions`: page through history for an `accountId`. You can
   narrow with `oldest-time`, `newest-time`, `min-amount`, `max-amount` and `text`.
5. `getBankingTransactionDetail`: get extended data for one `transactionId`.

Rules:
- Send `x-v` (the requested endpoint version) on every call. `x-min-v` is optional.
  When BOQ does not support the version, it returns HTTP 406 with
  `urn:au-cds:error:cds-all:Header/UnsupportedVersion`. This was seen live on the PRD host.
- Send `x-fapi-interaction-id`. When the customer is present, also send
  `x-fapi-auth-date` and `x-fapi-customer-ip-address`.
- Every operation is a read (GET, or a POST that only filters by a list of
  accountIds), so retrying is safe.
- Errors use the CDS `errors[]` envelope (`code`, `title`, `detail`, `meta.urn`).
