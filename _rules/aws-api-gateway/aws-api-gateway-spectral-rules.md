---
categories:
- deprecation
- info
- method
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
- tag
description: Spectral linting rules defining API design standards and conventions for Amazon API Gateway.
layout: rules
name: Amazon API Gateway API Rules
provider_name: Amazon API Gateway
provider_slug: aws-api-gateway
rule_count: 35
rules:
- description: API title must start with "Amazon API Gateway"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: Info object must have a description with at least 20 characters
  given: $.info
  name: info-description-required
  severity: error
- description: Info object must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info object should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: All specs must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers array must be defined and non-empty
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Each server should have a description
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Path segments must use kebab-case (lowercase letters, numbers, hyphens)
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Amazon API Gateway"
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: All tags used in operations should be defined in the global tags array
  given: $
  name: tag-global-defined
  severity: warn
- description: Global tags should have descriptions
  given: $.tags[*]
  name: tag-description
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: error
- description: All parameters must have a schema with a type
  given: $.paths[*][*].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Request bodies should have descriptions
  given: $.paths[*][*].requestBody
  name: request-body-description
  severity: warn
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Secured operations should document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-401-on-secured
  severity: warn
- description: Top-level component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description
  severity: warn
- description: Schema objects should define a type
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: Schema property names should use snake_case
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: info
- description: Security schemes must be defined in components
  given: $
  name: security-schemes-defined
  severity: error
- description: AWS SigV4 security scheme should be defined
  given: $.components.securitySchemes
  name: security-sigv4-scheme
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: method-get-no-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: method-delete-no-body
  severity: warn
- description: POST operations creating resources should have a request body
  given: $.paths[*].post
  name: method-post-has-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Deprecated operations should have a description explaining the deprecation
  given: $.paths[*][*][?(@.deprecated == true)]
  name: deprecation-documented
  severity: warn
rules_file: rules/aws-api-gateway-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-api-gateway/refs/heads/main/rules/aws-api-gateway-spectral-rules.yml
severity_counts:
  error: 17
  hint: 0
  info: 1
  warn: 17
slug: aws-api-gateway-spectral-rules
tags:
- API Gateway
- AWS
- Cloud
- REST
- WebSocket
- Serverless
- Spectral
- Linting
- API Governance
---
