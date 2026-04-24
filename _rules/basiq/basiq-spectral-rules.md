---
categories:
- basiq
description: Spectral linting rules defining API design standards and conventions for Basiq.
layout: rules
name: Basiq API Rules
provider_name: Basiq
provider_slug: basiq
rule_count: 15
rules:
- description: All protected operations must use BearerAuth security.
  given: $.paths[?(!@property.match('token'))].*.security
  name: basiq-bearer-auth-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths.*.*
  name: basiq-operation-id-required
  severity: error
- description: Operation IDs must use camelCase.
  given: $.paths.*.*.operationId
  name: basiq-operation-id-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths.*.*
  name: basiq-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: basiq-summary-title-case
  severity: warn
- description: All operations must be tagged.
  given: $.paths.*.*
  name: basiq-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths.*.*
  name: basiq-description-required
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths.*.get.responses
  name: basiq-200-response-required
  severity: error
- description: Parameterized path operations should define a 404 response.
  given: $.paths.*.get.responses
  name: basiq-404-response-required
  severity: warn
- description: User-scoped resource paths should be nested under /users/{userId}.
  given: $.paths[*]~
  name: basiq-user-path-prefix
  severity: warn
- description: Responses should reference schemas using $ref rather than inline definitions.
  given: $.paths.*.*.responses.*.content.application/json.schema
  name: basiq-response-schema-ref
  severity: warn
- description: All schema properties should have descriptions.
  given: $.components.schemas.*.properties.*
  name: basiq-schema-description-required
  severity: warn
- description: API info must include contact details.
  given: $.info
  name: basiq-info-contact-required
  severity: warn
- description: Server URLs must use HTTPS.
  given: $.servers.*.url
  name: basiq-server-url-https
  severity: error
- description: DELETE operations should return 204 No Content.
  given: $.paths.*.delete.responses
  name: basiq-204-delete-response
  severity: warn
rules_file: rules/basiq-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/basiq/refs/heads/main/rules/basiq-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 9
slug: basiq-spectral-rules
tags:
- Australia
- Banking
- CDR
- Financial Data
- Fintech
- Open Banking
- Transactions
- Spectral
- Linting
- API Governance
---
