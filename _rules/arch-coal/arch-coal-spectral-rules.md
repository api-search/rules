---
categories:
- get
- info
- openapi
- operation
- parameter
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Arch Coal.
layout: rules
name: Arch Coal API Rules
provider_name: Arch Coal
provider_slug: arch-coal
rule_count: 13
rules:
- description: API title must start with "Arch Coal"
  given: $.info
  name: info-title-arch-coal-prefix
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Use OpenAPI 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: Server URLs must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Arch Coal"
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-prefix
  severity: warn
- description: All operations must have tags
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: error
- description: Parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define success responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
rules_file: rules/arch-coal-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/arch-coal/refs/heads/main/rules/arch-coal-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 0
  warn: 3
slug: arch-coal-spectral-rules
tags:
- Mining
- Coal
- Metallurgical Coal
- Thermal Coal
- Energy
- Fortune 500
- Spectral
- Linting
- API Governance
---
