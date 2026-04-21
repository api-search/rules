---
categories:
- apis
- components
- examples
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- post
- request
- response
- schema
- servers
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for APIs.io.
layout: rules
name: APIs.io API Rules
provider_name: APIs.io
provider_slug: apis-io
rule_count: 37
rules:
- description: Info title should start with "APIs.io"
  given: $.info.title
  name: info-title-format
  severity: warn
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info should include contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Specs should use OpenAPI 3.1.x as established by the APIs.io API
  given: $.openapi
  name: openapi-version-31
  severity: warn
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "APIs.io"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Operation summaries should use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: info
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: OperationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Global tags array should be defined
  given: $
  name: tags-defined
  severity: warn
- description: All global tags should have descriptions
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: error
- description: All parameters must have a schema
  given: $.paths[*][*].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Parameter names should use snake_case
  given: $.paths[*][*].parameters[*].name
  name: parameter-names-snake-case
  severity: warn
- description: Request bodies should have descriptions
  given: $.paths[*][*].requestBody
  name: request-body-description-required
  severity: warn
- description: Request bodies should support application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: GET and POST operations must have a 2xx response
  given: $.paths[*][get,post]
  name: response-200-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Operations should include a 400 Bad Request response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-400-recommended
  severity: warn
- description: Operations should include a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-recommended
  severity: warn
- description: Operations should include a 500 Internal Server Error response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-500-recommended
  severity: warn
- description: Schema property names should use snake_case
  given: $.components.schemas[*].properties[*]~
  name: schema-properties-snake-case
  severity: info
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
- description: Schema objects should have a type defined
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Security schemes should be defined in components
  given: $.components
  name: components-security-schemes-defined
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should have a request body
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: examples-on-schemas
  severity: info
- description: APIs submitted to APIs.io should follow APIs.json format
  given: $.paths[*][post].requestBody.content.application/json.schema
  name: apis-json-format-validation
  severity: info
rules_file: rules/apis-io-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apis-io/refs/heads/main/rules/apis-io-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 6
  warn: 18
slug: apis-io-spectral-rules
tags:
- API Aggregation
- API Directory
- API Discovery
- API Indexing
- API Rating
- API Search
- APIs.json
- Search Engine
- Spectral
- Linting
- API Governance
---
