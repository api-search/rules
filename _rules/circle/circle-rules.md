---
categories:
- circle
description: Spectral linting rules defining API design standards and conventions for Circle.
layout: rules
name: Circle API Rules
provider_name: Circle
provider_slug: circle
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: circle-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: circle-server-https
  severity: error
- description: api.circle.com servers must include /v1.
  given: $.servers[?(@.url && @.url.indexOf('api.circle.com') > -1)].url
  name: circle-server-base-path
  severity: warn
- description: A bearer-token security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: circle-bearer-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: circle-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: circle-operation-tags
  severity: warn
- description: POST operations should accept an X-Idempotency-Key header.
  given: $.paths[*].post
  name: circle-idempotency-key
  severity: warn
- description: Mutating operations should declare 4xx/5xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: circle-error-responses
  severity: warn
- description: Path parameters named "id" should be UUIDs.
  given: $.paths[*].*.parameters[?(@.in == 'path' && @.name == 'id')].schema
  name: circle-uuid-identifiers
  severity: info
rules_file: rules/circle-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/circle/refs/heads/main/rules/circle-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 4
slug: circle-rules
tags:
- Blockchain
- Compliance
- Cross-Chain
- Currency
- Money
- Payments
- Stablecoin
- Transfers
- USDC
- Wallets
- Spectral
- Linting
- API Governance
---
