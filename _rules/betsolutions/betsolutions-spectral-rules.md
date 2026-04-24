---
categories:
- get
- hash
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
- security
- servers
description: Spectral linting rules defining API design standards and conventions for BetSolutions.
layout: rules
name: BetSolutions API Rules
provider_name: BetSolutions
provider_slug: betsolutions
rule_count: 30
rules:
- description: API info must have a title.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should begin with "BetSolutions".
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
- description: Server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Server URLs should use a betsolutions.com domain.
  given: $.servers[*].url
  name: servers-betsolutions-domain
  severity: warn
- description: Path segments should use kebab-case.
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
- description: Operation summaries should start with "BetSolutions".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
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
- description: POST operations should have a request body.
  given: $.paths[*].post
  name: post-request-body-required
  severity: warn
- description: Request bodies should use application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: BetSolutions API requires SHA-256 hash parameter for authentication.
  given: $.paths[*][post].requestBody.content['application/json'].schema.properties
  name: hash-parameter-required
  severity: info
- description: Operations must define at least one 2xx success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Success responses should return application/json content.
  given: $.paths[*][get,post,put,patch,delete].responses['200'].content
  name: response-json-content
  severity: warn
- description: Operations should define a 401 unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-defined
  severity: warn
- description: Top-level schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema definitions should have an explicit type.
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: BetSolutions response schemas should include a success boolean field.
  given: $.components.schemas[*].properties
  name: schema-success-flag
  severity: info
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-scheme-defined
  severity: error
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/betsolutions-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/betsolutions/refs/heads/main/rules/betsolutions-spectral-rules.yml
severity_counts:
  error: 15
  hint: 0
  info: 2
  warn: 13
slug: betsolutions-spectral-rules
tags:
- Betting
- Casinos
- Gaming
- Gambling
- Slots
- Sports Betting
- Spectral
- Linting
- API Governance
---
