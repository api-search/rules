---
categories:
- api
- get
- info
- openapi
- operation
- parameter
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for BankruptcyWatch.
layout: rules
name: BankruptcyWatch API Rules
provider_name: BankruptcyWatch
provider_slug: bankruptcywatch
rule_count: 15
rules:
- description: Info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Operations should define 401 response
  given: $.paths[*][post,put,patch,delete]
  name: response-401-defined
  severity: warn
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: BankruptcyWatch APIs use API key authentication
  given: $.components.securitySchemes[*]
  name: api-key-auth
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All schemas should have a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
rules_file: rules/bankruptcywatch-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bankruptcywatch/refs/heads/main/rules/bankruptcywatch-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 6
slug: bankruptcywatch-spectral-rules
tags:
- Bankruptcy
- Compliance
- Court Data
- Legal
- Lending
- PACER
- Spectral
- Linting
- API Governance
---
