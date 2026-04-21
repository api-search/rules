---
categories:
- info
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Azure Functions.
layout: rules
name: Azure Functions API Rules
provider_name: Azure Functions
provider_slug: azure-functions
rule_count: 15
rules:
- description: API title must start with "Azure Functions"
  given: $.info.title
  name: info-title-format
  severity: warn
- description: Operation summaries must start with "Azure Functions"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Paths must not end with a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Must use OpenAPI 3.x or Swagger 2.x
  given: $
  name: openapi-version
  severity: warn
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Operations must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All inline parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[?(!@.$ref)]
  name: parameter-description-required
  severity: warn
- description: Top-level schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-description
  severity: info
- description: All tags used in operations should be defined globally
  given: $.tags
  name: tags-global-definition
  severity: info
- description: OperationIds should use consistent naming
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: info
- description: Security schemes should be defined
  given: $.components.securitySchemes
  name: security-defined
  severity: info
rules_file: rules/azure-functions-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/azure-functions/refs/heads/main/rules/azure-functions-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 4
  warn: 6
slug: azure-functions-spectral-rules
tags:
- Cloud
- Compute
- Event-Driven
- Functions
- Serverless
- Spectral
- Linting
- API Governance
---
