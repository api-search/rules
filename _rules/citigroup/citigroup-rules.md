---
categories:
- citi
description: Spectral linting rules defining API design standards and conventions for Citigroup.
layout: rules
name: Citigroup API Rules
provider_name: Citigroup
provider_slug: citigroup
rule_count: 6
rules:
- description: All Citi API servers MUST use HTTPS.
  given: $.servers[*].url
  name: citi-https-only
  severity: error
- description: Citi APIs MUST declare OAuth 2.0 security schemes.
  given: $.components.securitySchemes
  name: citi-oauth-required
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: citi-operation-id
  severity: error
- description: Operations MUST be tagged for product domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: citi-tag-required
  severity: warn
- description: Operations MUST have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: citi-summary-required
  severity: warn
- description: API info MUST contain a contact for security disclosures.
  given: $.info
  name: citi-info-contact
  severity: warn
rules_file: rules/citigroup-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/citigroup/refs/heads/main/rules/citigroup-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 3
slug: citigroup-rules
tags:
- Banking
- Financial Services
- FX
- Open Banking
- Payments
- Treasury
- Spectral
- Linting
- API Governance
---
