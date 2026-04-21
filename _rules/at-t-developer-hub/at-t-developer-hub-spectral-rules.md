---
categories:
- camara
- get
- info
- microcks
- 'no'
- openapi
- operation
- parameter
- paths
- post
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for AT&T Developer Hub.
layout: rules
name: AT&T Developer Hub API Rules
provider_name: AT&T Developer Hub
provider_slug: at-t-developer-hub
rule_count: 26
rules:
- description: API title must start with "AT&T"
  given: $.info.title
  name: info-title-pattern
  severity: warn
- description: API info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: API info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: API info should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Must use OpenAPI 3.0.x
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Summaries must start with "AT&T"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-att-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: operationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationid-camelcase
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: API should define an ErrorInfo schema in components for CAMARA compliance
  given: $.components.schemas
  name: camara-error-schema
  severity: warn
- description: Phone number parameters should document E.164 format requirement
  given: $.components.schemas[*].properties.phoneNumber
  name: camara-phone-number-e164
  severity: info
- description: Every parameter must have a description
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Operations using security should document 401 responses
  given: $.paths[*][post,get,delete][?(@.security)]
  name: response-401-defined
  severity: warn
- description: Operations should document 429 Too Many Requests responses for rate limiting
  given: $.paths[*][post]
  name: response-429-defined
  severity: info
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should have a request body
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: Operations should include x-microcks-operation for mock server support
  given: $.paths[*][post,get,delete]
  name: microcks-operation-extension
  severity: info
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
rules_file: rules/at-t-developer-hub-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/at-t-developer-hub/refs/heads/main/rules/at-t-developer-hub-spectral-rules.yml
severity_counts:
  error: 14
  hint: 0
  info: 3
  warn: 9
slug: at-t-developer-hub-spectral-rules
tags:
- 5G
- Network APIs
- CAMARA
- Connectivity
- Telecommunications
- Edge Computing
- Device Status
- SIM Swap
- Spectral
- Linting
- API Governance
---
