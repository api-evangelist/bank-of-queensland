# Bank of Queensland (bank-of-queensland)

Bank of Queensland Limited (ASX: BOQ) is one of Australia's oldest banks, founded in Brisbane in 1874, and today an APRA-regulated authorised deposit-taking institution (ADI) and ASX-listed regional retail and commercial bank - a publicly listed company, not a customer-owned mutual. Its banking group includes the ME Bank, Virgin Money Australia and BOQ Specialist brands. As an accredited Consumer Data Right (CDR) data holder, BOQ exposes a public, unauthenticated Product Reference Data (PRD) API that conforms to the Australian Consumer Data Standards, while consumer data sharing runs through the regulated CDR / Accredited Data Recipient (ADR) model with OAuth2 / OIDC (FAPI) authorization.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/bank-of-queensland/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/bank-of-queensland/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- Product Reference Data
- ADI

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### Bank of Queensland (BOQ) CDR Product Reference Data API

Public, unauthenticated Consumer Data Right (CDR) Product Reference Data API exposing BOQ's banking products (accounts, term deposits, loans, cards) in machine-readable form under the Australian Consumer Data Standards. Confirmed live at `https://secure.api.boq.com.au/cds-au/v1/banking/products` (HTTP 200, x-v 3) returning a `data.products` array. Endpoints - `GET /banking/products` and `GET /banking/products/{productId}`.

- **Human URL:** [https://www.boq.com.au/personal/help-and-support/forms-and-important-information/open-banking](https://www.boq.com.au/personal/help-and-support/forms-and-important-information/open-banking)
- **Base URL:** `https://secure.api.boq.com.au/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking
- Australia

#### Properties

- [Documentation](https://www.boq.com.au/personal/help-and-support/forms-and-important-information/open-banking)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#product-reference-data)
- [OpenAPI](openapi/bank-of-queensland-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.boq.com.au/)
- [Documentation](https://www.boq.com.au/personal/help-and-support/forms-and-important-information/open-banking)
- [LinkedIn](https://www.linkedin.com/company/bank-of-queensland)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
