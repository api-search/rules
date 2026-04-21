---
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Avalara.
layout: rules
name: Avalara API Rules
provider_name: Avalara
provider_slug: avalara
rule_count: 21
rules:
- description: API title should reference Avalara or a named product
  given: $.info.title
  name: info-title-avalara-prefix
  severity: warn
- description: API info description must be present and non-empty
  given: $.info
  name: info-description-required
  severity: error
- description: API version must be present
  given: $.info
  name: info-version-required
  severity: error
- description: API contact information should be provided
  given: $.info
  name: info-contact-required
  severity: warn
- description: OpenAPI version must be 3.x
  given: $
  name: openapi-version-3x
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Paths should not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Paths should not contain query strings
  given: $.paths[*]~
  name: paths-no-query-strings
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Avalara
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-avalara-prefix
  severity: info
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Request bodies should include application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-on-top-level
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/avalara-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/avalara/refs/heads/main/rules/avalara-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 2
  warn: 9
slug: avalara-spectral-rules
tags:
- Taxes
- Spectral
- Linting
- API Governance
---
