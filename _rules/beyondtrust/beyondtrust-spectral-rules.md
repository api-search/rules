---
categories:
- credential
- http
- info
- 'no'
- openapi
- operation
- parameter
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for BeyondTrust.
layout: rules
name: BeyondTrust API Rules
provider_name: BeyondTrust
provider_slug: beyondtrust
rule_count: 23
rules:
- description: API title should start with "BeyondTrust"
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
  name: openapi-version-3
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "BeyondTrust"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
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
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Response descriptions are required
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Auth endpoints should return 401 on failure
  given: $.paths[*][post].responses
  name: response-401-for-auth
  severity: info
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema names should use PascalCase
  given: $.components.schemas
  name: schema-pascal-case-names
  severity: info
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security should be defined
  given: $
  name: security-global-defined
  severity: warn
- description: GET operations should not have request bodies
  given: $.paths[*].get
  name: http-get-no-body
  severity: error
- description: DELETE operations should not have request bodies
  given: $.paths[*].delete
  name: http-delete-no-body
  severity: warn
- description: Credential retrieval endpoints must require authentication
  given: $.paths['/requests/{requestId}/credentials'].get
  name: credential-endpoint-secured
  severity: error
- description: Descriptions should not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/beyondtrust-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/beyondtrust/refs/heads/main/rules/beyondtrust-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 2
  warn: 11
slug: beyondtrust-spectral-rules
tags:
- Access
- Access Management
- Compliance
- Credentials
- Privileged Access
- Security
- Secrets
- Zero Trust
- Spectral
- Linting
- API Governance
---
