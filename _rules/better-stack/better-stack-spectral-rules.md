---
categories:
- examples
- http
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Better Stack.
layout: rules
name: Better Stack API Rules
provider_name: Better Stack
provider_slug: better-stack
rule_count: 37
rules:
- description: API title should start with "Better Stack"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: API description should be at least 30 characters
  given: $.info.description
  name: info-description-min-length
  severity: warn
- description: API info must specify a version
  given: $.info
  name: info-version-required
  severity: error
- description: OpenAPI version should be 3.0.x
  given: $.openapi
  name: openapi-version
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Each server should have a description
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: Query strings must not appear in paths
  given: $.paths
  name: paths-no-query-string
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Better Stack"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined
  given: $
  name: tags-global-defined
  severity: info
- description: Each global tag should have a description
  given: $.tags[*]
  name: tags-description-required
  severity: info
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Query parameter names should use snake_case
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in=='query')].name
  name: parameter-snake-case
  severity: info
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Every operation must define a 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-defined
  severity: info
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema property names should use snake_case
  given: $.components.schemas[*].properties
  name: schema-property-snake-case
  severity: info
- description: Global security must be defined
  given: $
  name: security-global-defined
  severity: warn
- description: Security schemes must be defined in components
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Better Stack API should use Bearer authentication
  given: $.components.securitySchemes
  name: security-bearer-auth
  severity: info
- description: GET operations should not have a request body
  given: $.paths[*].get
  name: http-get-no-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: http-delete-no-body
  severity: warn
- description: POST operations should have a request body
  given: $.paths[*].post
  name: http-post-has-body
  severity: warn
- description: PATCH operations should have a request body
  given: $.paths[*].patch
  name: http-patch-has-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Schema properties should include example values
  given: $.components.schemas[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/better-stack-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/better-stack/refs/heads/main/rules/better-stack-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 7
  warn: 17
slug: better-stack-spectral-rules
tags:
- Incidents
- Logs
- Monitoring
- Platform
- Status
- Uptime
- Observability
- On-Call
- Heartbeats
- Spectral
- Linting
- API Governance
---
