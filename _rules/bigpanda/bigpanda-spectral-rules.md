---
categories:
- bigpanda
description: Spectral linting rules defining API design standards and conventions for BigPanda.
layout: rules
name: BigPanda API Rules
provider_name: BigPanda
provider_slug: bigpanda
rule_count: 23
rules:
- description: API title must start with "BigPanda"
  given: $.info.title
  name: bigpanda-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: bigpanda-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: bigpanda-info-contact-present
  severity: warn
- description: Operation summaries must start with "BigPanda"
  given: $.paths[*][*].summary
  name: bigpanda-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: bigpanda-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: bigpanda-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: bigpanda-operation-description-present
  severity: warn
- description: Paths must not end with a slash
  given: $.paths
  name: bigpanda-path-no-trailing-slash
  severity: warn
- description: POST operations must have a request body
  given: $.paths[*].post
  name: bigpanda-request-body-required
  severity: error
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: bigpanda-response-success-present
  severity: error
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: bigpanda-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: bigpanda-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: bigpanda-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: bigpanda-security-scheme-present
  severity: error
- description: Security scheme must be bearer auth
  given: $.components.securitySchemes[*]
  name: bigpanda-bearer-auth-used
  severity: warn
- description: Operations must declare security
  given: $.paths[*][get,post,put,patch,delete]
  name: bigpanda-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: bigpanda-tags-defined
  severity: warn
- description: API must define servers
  given: $
  name: bigpanda-servers-present
  severity: error
- description: Server URL must use HTTPS
  given: $.servers[*].url
  name: bigpanda-server-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: bigpanda-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: bigpanda-microcks-operation-present
  severity: warn
- description: Alert requests must include app_key field
  given: $.components.schemas.AlertRequest.required
  name: bigpanda-alert-app-key-required
  severity: warn
- description: API info must include license
  given: $.info
  name: bigpanda-license-present
  severity: warn
rules_file: rules/bigpanda-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bigpanda/refs/heads/main/rules/bigpanda-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 15
slug: bigpanda-spectral-rules
tags:
- Incidents
- Monitoring
- Platform
- Spectral
- Linting
- API Governance
---
