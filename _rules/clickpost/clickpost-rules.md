---
categories:
- clickpost
description: Spectral linting rules defining API design standards and conventions for ClickPost.
layout: rules
name: ClickPost API Rules
provider_name: ClickPost
provider_slug: clickpost
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: clickpost-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clickpost-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clickpost-server-https
  severity: error
- description: A security scheme (apiKey for token authentication) must be declared.
  given: $.components.securitySchemes
  name: clickpost-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickpost-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickpost-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickpost-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clickpost-error-responses
  severity: warn
rules_file: rules/clickpost-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clickpost/refs/heads/main/rules/clickpost-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: clickpost-rules
tags:
- Carriers
- Delivery
- E-Commerce Logistics
- Logistics
- Returns
- Shipping
- Supply Chain
- Tracking
- Spectral
- Linting
- API Governance
---
