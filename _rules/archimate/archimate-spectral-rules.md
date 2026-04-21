---
categories:
- delete
- get
- info
- openapi
- operation
- parameter
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for ArchiMate.
layout: rules
name: ArchiMate API Rules
provider_name: ArchiMate
provider_slug: archimate
rule_count: 14
rules:
- description: API title must start with "ArchiMate"
  given: $.info
  name: info-title-archimate-prefix
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
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "ArchiMate"
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
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
rules_file: rules/archimate-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/archimate/refs/heads/main/rules/archimate-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 1
  warn: 3
slug: archimate-spectral-rules
tags:
- Enterprise Architecture
- Architecture Framework
- Modeling Language
- Business Architecture
- Technology Architecture
- Standard
- Open Group
- Spectral
- Linting
- API Governance
---
