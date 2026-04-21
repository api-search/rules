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
description: Spectral linting rules defining API design standards and conventions for Archer Daniels Midland.
layout: rules
name: Archer Daniels Midland API Rules
provider_name: Archer Daniels Midland
provider_slug: archer-daniels-midland
rule_count: 13
rules:
- description: API title must start with "Archer Daniels Midland"
  given: $.info
  name: info-title-adm-prefix
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
- description: Operation summaries should start with "Archer Daniels Midland"
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-prefix
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: error
- description: All parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
rules_file: rules/archer-daniels-midland-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/archer-daniels-midland/refs/heads/main/rules/archer-daniels-midland-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 0
  warn: 3
slug: archer-daniels-midland-spectral-rules
tags:
- Agriculture
- Food Processing
- Commodities
- Supply Chain
- Fortune 100
- Nutrition
- Spectral
- Linting
- API Governance
---
