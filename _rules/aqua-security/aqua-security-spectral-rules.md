---
categories:
- delete
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
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Aqua Security.
layout: rules
name: Aqua Security API Rules
provider_name: Aqua Security
provider_slug: aqua-security
rule_count: 30
rules:
- description: Info object must have a title starting with "Aqua Security"
  given: $.info
  name: info-title-required
  severity: error
- description: Info object must have a description with at least 50 characters
  given: $.info
  name: info-description-required
  severity: warn
- description: Info object must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: API should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Use OpenAPI 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs should use HTTPS
  given: $.servers[*]
  name: servers-https-only
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths should not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Aqua Security"
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-prefix
  severity: warn
- description: Every operation should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-required
  severity: error
- description: OperationId should use camelCase
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: error
- description: All parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameter names should use snake_case or kebab-case
  given: $.paths[*][*].parameters[*]
  name: parameter-snake-case
  severity: info
- description: Request bodies should use application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-type
  severity: warn
- description: Every operation must have a success (2xx) response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Secured endpoints should document 401 responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-401-required
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Schema properties should have a type defined
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
- description: Security schemes must be defined in components
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Bearer auth security scheme should have a description
  given: $.components.securitySchemes[*]
  name: security-bearer-description
  severity: warn
- description: GET operations should not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
- description: Descriptions should not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Tags should be defined globally with descriptions
  given: $
  name: tags-global-defined
  severity: warn
rules_file: rules/aqua-security-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aqua-security/refs/heads/main/rules/aqua-security-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 3
  warn: 15
slug: aqua-security-spectral-rules
tags:
- Cloud Native
- Containers
- Kubernetes
- Runtime Protection
- Security
- Vulnerability Scanning
- Spectral
- Linting
- API Governance
---
