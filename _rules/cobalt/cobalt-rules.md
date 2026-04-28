---
categories:
- cobalt
description: Spectral linting rules defining API design standards and conventions for Cobalt.
layout: rules
name: Cobalt API Rules
provider_name: Cobalt
provider_slug: cobalt
rule_count: 13
rules:
- description: API contact information must be present.
  given: $.info
  name: cobalt-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cobalt-info-license
  severity: warn
- description: API termsOfService link should be declared.
  given: $.info
  name: cobalt-info-terms
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cobalt-server-https
  severity: error
- description: Cobalt server URLs must include /api/v2.
  given: $.servers[?(@.url && @.url.indexOf('gocobalt.io') > -1)].url
  name: cobalt-server-versioned
  severity: warn
- description: An apiKey security scheme must be defined.
  given: $.components.securitySchemes
  name: cobalt-apikey-security
  severity: error
- description: All Cobalt API paths should live under /public.
  given: $.paths
  name: cobalt-public-path-prefix
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cobalt-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cobalt-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cobalt-operation-id
  severity: error
- description: Operation IDs should be camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: cobalt-operation-id-camelcase
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cobalt-error-responses
  severity: warn
- description: List endpoints should expose page/limit pagination.
  given: $.paths[?(@property.match(/linked-account$|application$|execution$|records$/))].get.parameters[*].name
  name: cobalt-pagination-page-limit
  severity: info
rules_file: rules/cobalt-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cobalt/refs/heads/main/rules/cobalt-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 8
slug: cobalt-rules
tags:
- Automation
- Embedded iPaaS
- Integrations
- Spectral
- Linting
- API Governance
---
