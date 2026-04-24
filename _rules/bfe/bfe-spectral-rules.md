---
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for BFE.
layout: rules
name: BFE API Rules
provider_name: BFE
provider_slug: bfe
rule_count: 22
rules:
- description: API info must have a title.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should begin with "BFE".
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API info must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: API info must have a version.
  given: $.info
  name: info-version-required
  severity: error
- description: All specs must use OpenAPI 3.0.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: BFE management API may use localhost (HTTP) for internal endpoints.
  given: $.servers[*].url
  name: servers-localhost-or-http
  severity: info
- description: Path segments should use kebab-case (lowercase with hyphens).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-summary-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-description-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-tags-required
  severity: error
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define at least one 2xx success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Success responses should return application/json content.
  given: $.paths[*][get,post,put,patch,delete].responses['200','201'].content
  name: response-json-content
  severity: warn
- description: Top-level schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema definitions should have an explicit type.
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/bfe-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bfe/refs/heads/main/rules/bfe-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 1
  warn: 8
slug: bfe-spectral-rules
tags:
- Load Balancer
- Networking
- Open Source
- Traffic Management
- CNCF
- Baidu
- Spectral
- Linting
- API Governance
---
