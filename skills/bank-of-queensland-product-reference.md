---
name: Look up Bank of Queensland banking products (CDR PRD)
description: >-
  Discover and inspect BOQ banking products (accounts, term deposits, loans,
  cards) through the public, unauthenticated Consumer Data Right Product
  Reference Data API. No credentials required - only the mandatory x-v header.
api: openapi/bank-of-queensland-cds-banking-products-openapi.yml
base_url: https://secure.api.boq.com.au/cds-au/v1
auth: none
operations:
  - listBankingProducts
  - getBankingProductDetail
---

# Look up Bank of Queensland banking products

BOQ exposes its product catalogue through the mandated CDR **Product Reference
Data (PRD)** API. It is **public and unauthenticated** - no API key, OAuth token
or CDR accreditation is needed for these two operations. Every request MUST send
the `x-v` version header (use `x-v: 3`, confirmed live).

Base URL: `https://secure.api.boq.com.au/cds-au/v1`

## Step 1 - List products (`listBankingProducts`)

`GET /banking/products` with header `x-v: 3`.

Useful query parameters:
- `product-category` - filter to one `BankingProductCategory` (e.g. `TERM_DEPOSITS`, `TRANS_AND_SAVINGS_ACCOUNTS`).
- `brand` - filter by brand (`BOQ`, `ME Bank`, `Virgin Money`, `BOQ Specialist`).
- `effective` - `CURRENT` (default), `FUTURE`, or `ALL`.
- `updated-since` - only products updated after a given DateTimeString.
- `page` / `page-size` - standard pagination (default page 1, size 25).

Read the response `data.products[]` array and `meta.totalRecords` /
`meta.totalPages`; follow `links.next` to page through the full catalogue.

## Step 2 - Get product detail (`getBankingProductDetail`)

For any `productId` returned in step 1, call
`GET /banking/products/{productId}` with header `x-v: 3`. The detail payload
embeds `features`, `constraints`, `fees`, `depositRates`, `lendingRates`,
`eligibility`, and `bundles` arrays - each element carries a `type`/`featureType`
enum plus a generic `additionalValue` field whose meaning depends on that type.

## Rules & conventions

- **Versioning:** always send `x-v: 3`. A missing header returns
  `urn:au-cds:error:cds-all:Header/MissingRequiredHeader` (400); an unsupported
  version returns `urn:au-cds:error:cds-all:Header/UnsupportedVersion` (406).
- **Errors** use the CDS `ResponseErrorListV2` envelope (`errors[]` with
  `urn:au-cds:...` codes), **not** RFC 9457. See
  `errors/bank-of-queensland-problem-types.yml`.
- **No idempotency key** is needed - these are read-only GETs.
- **Do not** attempt account, balance, transaction, payee or payment endpoints
  here: they require CDR Accredited Data Recipient authorization (OAuth2/FAPI)
  and are not open to arbitrary developers. See
  `authentication/bank-of-queensland-authentication.yml`.
