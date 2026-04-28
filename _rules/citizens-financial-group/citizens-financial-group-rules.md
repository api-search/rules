---
categories:
- citizens
description: Spectral linting rules defining API design standards and conventions for Citizens Financial Group.
layout: rules
name: Citizens Financial Group API Rules
provider_name: Citizens Financial Group
provider_slug: citizens-financial-group
rule_count: 6
rules:
- description: All Citizens API servers MUST use HTTPS.
  given: $.servers[*].url
  name: citizens-https-only
  severity: error
- description: Citizens APIs MUST declare an OAuth 2.0 security scheme for consented data access.
  given: $.components.securitySchemes
  name: citizens-oauth-required
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: citizens-operation-id
  severity: error
- description: Operations MUST be tagged for product domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: citizens-tag-required
  severity: warn
- description: API info MUST contain a contact for security disclosures.
  given: $.info
  name: citizens-info-contact
  severity: warn
- description: Open banking endpoints SHOULD align with Financial Data Exchange (FDX) field names.
  given: $.components.schemas
  name: citizens-fdx-alignment
  severity: warn
rules_file: rules/citizens-financial-group-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/citizens-financial-group/refs/heads/main/rules/citizens-financial-group-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 3
slug: citizens-financial-group-rules
tags:
- Banking
- Buy Now Pay Later
- Financial Services
- FDX
- Locator
- Open Banking
- Payments
- Spectral
- Linting
- API Governance
---
