---
categories:
- get
- info
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Bandwidth.
layout: rules
name: Bandwidth API Rules
provider_name: Bandwidth
provider_slug: bandwidth
rule_count: 16
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
- description: Operation summaries should start with "Bandwidth"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-bandwidth-prefix
  severity: info
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
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
rules_file: rules/bandwidth-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bandwidth/refs/heads/main/rules/bandwidth-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 1
  warn: 6
slug: bandwidth-spectral-rules
tags:
- Communications
- CPaaS
- Voice
- Messaging
- Telephony
- SMS
- MFA
- Spectral
- Linting
- API Governance
---
