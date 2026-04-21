---
categories:
- components
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
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Backblaze.
layout: rules
name: Backblaze API Rules
provider_name: Backblaze
provider_slug: backblaze
rule_count: 31
rules:
- description: Info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info should have contact information
  given: $.info
  name: info-contact-required
  severity: info
- description: Must use OpenAPI 3.0.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: B2 Native API paths should use /b2api/v{version}/ prefix
  given: $.paths
  name: paths-b2-api-prefix
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: Operation summaries should start with "Backblaze B2"
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-backblaze-prefix
  severity: info
- description: Global tags array should be defined
  given: $
  name: tags-global-defined
  severity: info
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should have descriptions
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: info
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Operations with auth should define 401 response
  given: $.paths[*][post,get]
  name: response-401-defined
  severity: warn
- description: All schemas should have a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: All component schemas should have a title
  given: $.components.schemas[*]
  name: schema-title-defined
  severity: info
- description: All component schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-defined
  severity: info
- description: Security schemes must be defined in components
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security should be defined
  given: $
  name: security-global-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should have a request body
  given: $.paths[*].post
  name: post-b2-operations-have-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Spec should define reusable schemas in components
  given: $.components
  name: components-schemas-present
  severity: info
rules_file: rules/backblaze-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/backblaze/refs/heads/main/rules/backblaze-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 7
  warn: 12
slug: backblaze-spectral-rules
tags:
- Cloud Storage
- Object Storage
- Storage
- Backup
- Spectral
- Linting
- API Governance
---
