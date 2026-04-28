---
categories:
- cloudzero
description: Spectral linting rules defining API design standards and conventions for CloudZero.
layout: rules
name: CloudZero API Rules
provider_name: CloudZero
provider_slug: cloudzero
rule_count: 12
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudzero-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudzero-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudzero-server-https
  severity: error
- description: Server URL must reference api.cloudzero.com.
  given: $.servers[*].url
  name: cloudzero-server-host
  severity: warn
- description: An apiKey security scheme must be defined.
  given: $.components.securitySchemes
  name: cloudzero-api-key-auth
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudzero-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudzero-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudzero-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudzero-error-responses
  severity: warn
- description: List endpoints should accept page and page_size query parameters.
  given: $.paths[?(@property.match(/insights$|budgets$|costs$|dimensions$/))].get.parameters[*].name
  name: cloudzero-pagination-page
  severity: info
- description: Date parameters and properties should use ISO 8601 (date or date-time).
  given: $..[?(@property === 'start_date' || @property === 'end_date')].schema
  name: cloudzero-iso-date
  severity: warn
- description: Currency fields should use ISO 4217 codes.
  given: $..[?(@property === 'currency')].schema
  name: cloudzero-currency-iso
  severity: warn
rules_file: rules/cloudzero-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudzero/refs/heads/main/rules/cloudzero-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 7
slug: cloudzero-rules
tags:
- Budgets
- Cloud Cost Management
- Cost Allocation
- Cost Optimization
- FinOps
- Telemetry
- Unit Economics
- Spectral
- Linting
- API Governance
---
