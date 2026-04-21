---
categories:
- http
- info
- microcks
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Appium.
layout: rules
name: Appium API Rules
provider_name: Appium
provider_slug: appium
rule_count: 27
rules:
- description: Info title must be present and follow "Appium ..." pattern
  given: $.info
  name: info-title-required
  severity: error
- description: Info description must be present and have minimum length
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: License information must be present (Appium is Apache 2.0)
  given: $.info
  name: info-license-required
  severity: warn
- description: OpenAPI version must be 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Each server must have a description
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments must use kebab-case (lowercase, hyphens)
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
- description: Operation summary must start with "Appium"
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-appium-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Every operation must have a 2xx response defined
  given: $.paths[*][get,post,put,patch,delete].responses
  name: operation-success-response-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Component schemas must have a title
  given: $.components.schemas[*]
  name: schema-title-required
  severity: warn
- description: Schema property names should use camelCase or snake_case consistently
  given: $.components.schemas[*].properties
  name: schema-properties-snake-case
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: http-get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: http-delete-no-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Operations should include x-microcks-operation extension for mock server compatibility
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
rules_file: rules/appium-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/appium/refs/heads/main/rules/appium-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 2
  warn: 15
slug: appium-spectral-rules
tags:
- Android
- Cross-Platform
- iOS
- Mobile Testing
- Open Source
- OpenJS Foundation
- Test Automation
- WebDriver
- Spectral
- Linting
- API Governance
---
