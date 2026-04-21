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
description: Spectral linting rules defining API design standards and conventions for ArcBest.
layout: rules
name: ArcBest API Rules
provider_name: ArcBest
provider_slug: arcbest
rule_count: 18
rules:
- description: API title must start with "ArcBest"
  given: $.info
  name: info-title-arcbest-prefix
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: API must specify a version
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
- description: Operation summaries should start with "ArcBest"
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-prefix
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
- description: All secured endpoints should document 401 responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-401-secured
  severity: warn
- description: Schema properties should define a type
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
rules_file: rules/arcbest-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/arcbest/refs/heads/main/rules/arcbest-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 1
  warn: 6
slug: arcbest-spectral-rules
tags:
- Logistics
- Freight
- LTL
- Supply Chain
- Shipping
- Transportation
- Spectral
- Linting
- API Governance
---
