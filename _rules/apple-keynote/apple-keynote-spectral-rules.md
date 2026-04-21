---
categories:
- http
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apple Keynote.
layout: rules
name: Apple Keynote API Rules
provider_name: Apple Keynote
provider_slug: apple-keynote
rule_count: 22
rules:
- description: API info title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Apple Keynote"
  given: $.info
  name: info-title-apple-prefix
  severity: warn
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: API description must be present with minimum length
  given: $.info
  name: info-description-required
  severity: warn
- description: OpenAPI version must be 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summary must start with "Apple Keynote"
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-apple-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: operation-success-response-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas must have a title
  given: $.components.schemas[*]
  name: schema-title-required
  severity: warn
- description: Component schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: http-get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apple-keynote-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apple-keynote/refs/heads/main/rules/apple-keynote-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 13
slug: apple-keynote-spectral-rules
tags:
- Apple
- Design
- iWork
- Presentations
- Productivity
- Slides
- Spectral
- Linting
- API Governance
---
