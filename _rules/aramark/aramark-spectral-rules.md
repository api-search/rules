---
categories:
- delete
- get
- info
- openapi
- operation
- parameter
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Aramark.
layout: rules
name: Aramark API Rules
provider_name: Aramark
provider_slug: aramark
rule_count: 21
rules:
- description: API title must start with "Aramark"
  given: $.info
  name: info-title-aramark-prefix
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: API must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Use OpenAPI 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: Server URLs must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Aramark"
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-aramark-prefix
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: error
- description: All parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All secured operations should document 401 responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-401-required
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-described
  severity: info
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: API key should be passed in the header (not query)
  given: $.components.securitySchemes[*][?(@.type=='apiKey')]
  name: security-api-key-header
  severity: error
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
rules_file: rules/aramark-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aramark/refs/heads/main/rules/aramark-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 2
  warn: 6
slug: aramark-spectral-rules
tags:
- Food Services
- Facilities Management
- Uniform Services
- Data Platform
- Fortune 500
- Spectral
- Linting
- API Governance
---
