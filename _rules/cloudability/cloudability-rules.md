---
categories:
- cloudability
description: Spectral linting rules defining API design standards and conventions for Cloudability.
layout: rules
name: Cloudability API Rules
provider_name: Cloudability
provider_slug: cloudability
rule_count: 11
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudability-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudability-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudability-server-https
  severity: error
- description: API server URLs must include /v3.
  given: $.servers[?(@.url && @.url.indexOf('cloudability.com') > -1)].url
  name: cloudability-server-versioned
  severity: warn
- description: A basic-auth security scheme (API token) must be defined.
  given: $.components.securitySchemes
  name: cloudability-basic-auth
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudability-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudability-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudability-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudability-error-responses
  severity: warn
- description: List endpoints should accept limit and offset query params.
  given: $.paths[?(@property.match(/list$|reports$|recommendations$|anomalies$|business-mappings$/))].get.parameters[*].name
  name: cloudability-pagination-limit-offset
  severity: info
- description: Currency parameters and properties should use ISO 4217 codes.
  given: $..[?(@property === 'currency')].schema
  name: cloudability-currency-iso
  severity: warn
rules_file: rules/cloudability-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudability/refs/heads/main/rules/cloudability-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 6
slug: cloudability-rules
tags:
- Cloud Cost Management
- Cost Optimization
- FinOps
- Multi-Cloud
- Recommendations
- Reporting
- Spectral
- Linting
- API Governance
---
