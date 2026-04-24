---
categories:
- truist
description: Spectral linting rules defining API design standards and conventions for BB&T Corp (Truist).
layout: rules
name: BB&T Corp (Truist) API Rules
provider_name: BB&T Corp (Truist)
provider_slug: bbandt-corp
rule_count: 5
rules:
- description: All Truist API operations must use OAuth 2.0 Bearer authentication.
  given: $.paths.*.*.security
  name: truist-bearer-auth-required
  severity: error
- description: All Truist API operations must have an operationId.
  given: $.paths.*.*
  name: truist-operation-id-required
  severity: error
- description: All GET operations should define a 200 success response.
  given: $.paths.*.get.responses
  name: truist-response-200-required
  severity: warn
- description: Operations should define standard error responses.
  given: $.paths.*.*.responses
  name: truist-error-responses-defined
  severity: info
- description: List operations should support pagination parameters.
  given: $.paths[?(@property.match('accounts|transactions'))].get.parameters
  name: truist-pagination-parameters
  severity: info
rules_file: rules/bbandt-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bbandt-corp/refs/heads/main/rules/bbandt-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 1
slug: bbandt-spectral-rules
tags:
- Banking
- Financial Services
- Open Banking
- Truist
- BB&T
- Spectral
- Linting
- API Governance
---
