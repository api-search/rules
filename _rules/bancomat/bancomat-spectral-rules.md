---
categories:
- bancomat
description: Spectral linting rules defining API design standards and conventions for Bancomat.
layout: rules
name: Bancomat API Rules
provider_name: Bancomat
provider_slug: bancomat
rule_count: 10
rules:
- description: API title must be present.
  given: $.info
  name: bancomat-info-title-required
  severity: error
- description: API description must be present.
  given: $.info
  name: bancomat-info-description-required
  severity: warn
- description: API version must be present.
  given: $.info
  name: bancomat-info-version-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: bancomat-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: bancomat-operation-summary-required
  severity: warn
- description: Payment endpoints must return a status field.
  given: $.components.schemas.Payment.properties
  name: bancomat-payment-status-response
  severity: warn
- description: All BANCOMAT APIs must define security schemes.
  given: $
  name: bancomat-security-required
  severity: error
- description: GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: bancomat-response-200-required
  severity: error
- description: Error responses must include a schema.
  given: $.paths[*][*].responses[4XX].content[*]
  name: bancomat-error-response-schema
  severity: warn
- description: All named schemas must have a description.
  given: $.components.schemas[*]
  name: bancomat-schema-description-required
  severity: warn
rules_file: rules/bancomat-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bancomat/refs/heads/main/rules/bancomat-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: bancomat-spectral-rules
tags:
- ATM
- Banking
- Financial Services
- Italy
- Mobile Payments
- Payments
- Debit Cards
- Spectral
- Linting
- API Governance
---
