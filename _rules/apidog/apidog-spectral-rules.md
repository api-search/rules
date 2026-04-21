---
categories:
- info
- openapi
- operation
- parameter
- paths
- post
- response
- security
- servers
- tag
description: Spectral linting rules defining API design standards and conventions for Apidog.
layout: rules
name: Apidog API Rules
provider_name: Apidog
provider_slug: apidog
rule_count: 20
rules:
- description: API title must start with 'Apidog'.
  given: $.info
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: API must have a version.
  given: $.info
  name: info-version-required
  severity: error
- description: Specs must use OpenAPI 3.x.
  given: $
  name: openapi-version-3
  severity: warn
- description: Servers must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Path segments must use kebab-case.
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with 'Apidog'.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-camelcase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: All tags must have a description.
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Protected operations should have a 401 response.
  given: $.paths[*][post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-scheme-defined
  severity: error
- description: POST operations should have a request body.
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
rules_file: rules/apidog-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apidog/refs/heads/main/rules/apidog-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 12
slug: apidog-spectral-rules
tags:
- API Design
- API Lifecycle
- API Testing
- Collaboration
- Design-First
- Documentation
- Mocking
- Platform
- Spectral
- Linting
- API Governance
---
