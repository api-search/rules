---
categories:
- bancontact
description: Spectral linting rules defining API design standards and conventions for Bancontact.
layout: rules
name: Bancontact API Rules
provider_name: Bancontact
provider_slug: bancontact
rule_count: 12
rules:
- description: API title must be present.
  given: $.info
  name: bancontact-info-title-required
  severity: error
- description: API description must be present.
  given: $.info
  name: bancontact-info-description-required
  severity: warn
- description: API version must be present.
  given: $.info
  name: bancontact-info-version-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: bancontact-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: bancontact-operation-summary-required
  severity: warn
- description: Payment response schemas must include a status field.
  given: $.components.schemas.Payment.properties
  name: bancontact-payment-status-field
  severity: warn
- description: Payment request schemas must include amount.
  given: $.components.schemas.PaymentRequest.properties
  name: bancontact-payment-amount-required
  severity: error
- description: All Bancontact APIs must define security schemes.
  given: $
  name: bancontact-security-required
  severity: error
- description: Payment operations should document webhook callbacks.
  given: $.paths[*].post
  name: bancontact-webhook-callback
  severity: info
- description: POST operations should return 201 on resource creation.
  given: $.paths[*].post.responses
  name: bancontact-response-201-for-post
  severity: warn
- description: Error responses must include a schema.
  given: $.paths[*][*].responses[4XX].content[*]
  name: bancontact-error-response-schema
  severity: warn
- description: All named schemas must have a description.
  given: $.components.schemas[*]
  name: bancontact-schema-description-required
  severity: warn
rules_file: rules/bancontact-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bancontact/refs/heads/main/rules/bancontact-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 6
slug: bancontact-spectral-rules
tags:
- Banking
- Belgium
- Debit Cards
- E-Commerce
- Fintech
- Payments
- Spectral
- Linting
- API Governance
---
