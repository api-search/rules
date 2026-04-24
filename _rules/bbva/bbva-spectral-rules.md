---
categories:
- bbva
description: Spectral linting rules defining API design standards and conventions for BBVA.
layout: rules
name: BBVA API Rules
provider_name: BBVA
provider_slug: bbva
rule_count: 6
rules:
- description: BBVA API operations must use OAuth 2.0 Bearer token authentication.
  given: $.paths[?(!@property.match('(token|oauth)'))].*.security
  name: bbva-bearer-auth-required
  severity: error
- description: All BBVA API operations must have an operationId.
  given: $.paths.*.*
  name: bbva-operation-id-required
  severity: error
- description: All GET operations should define a 200 success response.
  given: $.paths.*.get.responses
  name: bbva-response-200-required
  severity: warn
- description: Operations should define a 400 error response for bad requests.
  given: $.paths.*.*.responses
  name: bbva-error-response-400
  severity: warn
- description: BBVA multi-country APIs should document country selection mechanism.
  given: $.info
  name: bbva-country-header-documented
  severity: info
- description: IBAN fields should use string format with pattern constraint.
  given: $.components.schemas..[?(@property === 'iban')]
  name: bbva-iban-format
  severity: warn
rules_file: rules/bbva-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bbva/refs/heads/main/rules/bbva-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 3
slug: bbva-spectral-rules
tags:
- Banking
- Financial Services
- Open Banking
- PSD2
- Spain
- Mexico
- Spectral
- Linting
- API Governance
---
