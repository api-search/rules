---
categories:
- http
- info
- 'no'
- openapi
- operation
- pagination
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for BetterCloud.
layout: rules
name: BetterCloud API Rules
provider_name: BetterCloud
provider_slug: bettercloud
rule_count: 28
rules:
- description: API title should start with "BetterCloud"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: API must specify a version
  given: $.info
  name: info-version-required
  severity: error
- description: Should use OpenAPI 3.0.x
  given: $.openapi
  name: openapi-version
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "BetterCloud"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: Operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameters must have schemas
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Response descriptions are required
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Error schema must have code, id, href, and reason fields
  given: $.components.schemas.ErrorResponse.required
  name: schema-error-required-fields
  severity: error
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security should be defined
  given: $
  name: security-global-defined
  severity: warn
- description: BetterCloud uses API key in header (X-API-Key)
  given: $.components.securitySchemes[*][?(@.type=='apiKey')]
  name: security-api-key-header
  severity: info
- description: GET operations should not have request bodies
  given: $.paths[*].get
  name: http-get-no-body
  severity: error
- description: DELETE operations should not have request bodies
  given: $.paths[*].delete
  name: http-delete-no-body
  severity: warn
- description: POST operations creating resources should have request bodies
  given: $.paths[*].post
  name: http-post-has-body
  severity: warn
- description: List endpoints should support page parameter
  given: $.paths[*].get.parameters[?(@.name=='page')].schema.type
  name: pagination-page-parameter
  severity: info
- description: Descriptions should not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/bettercloud-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bettercloud/refs/heads/main/rules/bettercloud-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 2
  warn: 13
slug: bettercloud-spectral-rules
tags:
- Automation
- Compliance
- Enterprise
- IT Operations
- SaaS Management
- Security
- Workflows
- User Lifecycle
- Spectral
- Linting
- API Governance
---
