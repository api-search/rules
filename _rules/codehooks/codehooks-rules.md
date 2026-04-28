---
categories:
- codehooks
description: Spectral linting rules defining API design standards and conventions for Codehooks.
layout: rules
name: Codehooks API Rules
provider_name: Codehooks
provider_slug: codehooks
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: codehooks-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: codehooks-server-https
  severity: error
- description: Codehooks server URL must use the {projectId}.api.codehooks.io/{space} template.
  given: $.servers[?(@.url && @.url.indexOf('codehooks.io') > -1)].url
  name: codehooks-server-template
  severity: warn
- description: An API key security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: codehooks-apikey-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: codehooks-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: codehooks-operation-tags
  severity: warn
- description: Collection-level paths should be declared as /{collection} or sub-paths thereof.
  given: $.paths
  name: codehooks-collection-path
  severity: info
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: codehooks-error-responses
  severity: warn
- description: List endpoints should accept the q query parameter for MongoDB-style filters.
  given: $.paths['/{collection}'].get.parameters[*]
  name: codehooks-query-parameter
  severity: info
- description: List endpoints should accept the h hints query parameter (sort, fields, offset, limit).
  given: $.paths['/{collection}'].get.parameters[*].name
  name: codehooks-pagination-hints
  severity: info
rules_file: rules/codehooks-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/codehooks/refs/heads/main/rules/codehooks-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 3
  warn: 3
slug: codehooks-rules
tags:
- Backend
- Database
- Events
- Hooks
- JavaScript
- NoSQL
- Queues
- Serverless
- Webhooks
- Workers
- Workflows
- Spectral
- Linting
- API Governance
---
