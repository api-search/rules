---
categories:
- basetrip
description: Spectral linting rules defining API design standards and conventions for Basetrip.
layout: rules
name: Basetrip API Rules
provider_name: Basetrip
provider_slug: basetrip
rule_count: 15
rules:
- description: All operations must require X-API-Key header authentication.
  given: $.paths.*.*.security
  name: basetrip-api-key-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths.*.*
  name: basetrip-operation-id-required
  severity: error
- description: Operation IDs must use camelCase.
  given: $.paths.*.*.operationId
  name: basetrip-operation-id-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths.*.*
  name: basetrip-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: basetrip-summary-title-case
  severity: warn
- description: All operations must be tagged.
  given: $.paths.*.*
  name: basetrip-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths.*.*
  name: basetrip-description-required
  severity: warn
- description: All GET operations must have a 200 response.
  given: $.paths.*.get.responses
  name: basetrip-200-response-required
  severity: error
- description: Operations should document 401 Unauthorized responses.
  given: $.paths.*.get.responses
  name: basetrip-401-response-defined
  severity: warn
- description: Operations on parameterized paths should document 404 responses.
  given: $.paths[*~/*{id}*].*.responses
  name: basetrip-404-response-defined
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: basetrip-path-kebab-case
  severity: warn
- description: All schema properties should have descriptions.
  given: $.components.schemas.*.properties.*
  name: basetrip-schema-description-required
  severity: warn
- description: Responses should reference schemas using $ref rather than inline definitions.
  given: $.paths.*.*.responses.*.content.application/json.schema
  name: basetrip-response-schema-ref
  severity: warn
- description: API info must include contact details.
  given: $.info
  name: basetrip-info-contact-required
  severity: warn
- description: Server URLs must use HTTPS.
  given: $.servers.*.url
  name: basetrip-server-url-https
  severity: error
rules_file: rules/basetrip-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/basetrip/refs/heads/main/rules/basetrip-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 9
slug: basetrip-spectral-rules
tags:
- Cities
- Countries
- Health
- Safety
- Travel
- Visa
- Spectral
- Linting
- API Governance
---
