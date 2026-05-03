---
api_specs:
- filename: sage-accounting-openapi.yml
  format: yaml
  label: Sage Accounting API
  slug: accounting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sage/refs/heads/main/openapi/sage-accounting-openapi.yml
categories:
- sage
description: Spectral linting rules defining API design standards and conventions for Sage.
layout: rules
name: Sage API Rules
provider_name: Sage
provider_slug: sage
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sage-operation-summary-title-case
  severity: warn
- description: All endpoints must use OAuth2 authentication
  given: $.paths[*][*]
  name: sage-oauth2-security-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: sage-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: sage-tags-required
  severity: warn
- description: Sage API resource paths use snake_case
  given: $.paths
  name: sage-resource-paths-snake-case
  severity: info
- description: List endpoints should support items_per_page parameter
  given: $.paths[*][get]
  name: sage-list-pagination-items-per-page
  severity: info
- description: List responses should use $items array format
  given: $.components.schemas[*List]*
  name: sage-response-list-format
  severity: info
- description: API documentation should reference rate limiting
  given: $.info.description
  name: sage-rate-limit-documented
  severity: info
- description: OAuth2 security scheme must use authorizationCode flow
  given: $.components.securitySchemes[*].flows
  name: sage-oauth-authorization-code-flow
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*][delete].responses
  name: sage-response-delete-204
  severity: info
rules_file: rules/sage-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sage/refs/heads/main/rules/sage-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 5
  warn: 4
slug: sage-rules
source_filename: sage-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sage-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*)( [A-Z][a-z0-9]*)*$\"\n\n  sage-oauth2-security-required:\n    description: All endpoints must use OAuth2 authentication\n    message: \"Endpoint must declare OAuth2 security\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: security\n      function: defined\n\n  sage-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sage-tags-required:\n    description:\
  \ All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  sage-resource-paths-snake-case:\n    description: Sage API resource paths use snake_case\n    message: \"Sage API resource paths use snake_case (e.g., sales_invoices)\"\n    given: \"$.paths\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/[a-z_/{}]+$\"\n\n  sage-list-pagination-items-per-page:\n    description: List endpoints should support items_per_page parameter\n    message: \"List endpoints should define items_per_page query parameter\"\n    given: \"$.paths[*][get]\"\n    severity: info\n    then:\n      function: defined\n\n  sage-response-list-format:\n    description: List responses should use $items array format\n    message: \"List response schemas should have $items array\"\n    given: \"$.components.schemas[*List]*\"\
  \n    severity: info\n    then:\n      field: properties\n      function: defined\n\n  sage-rate-limit-documented:\n    description: API documentation should reference rate limiting\n    message: \"API info description should mention rate limits\"\n    given: \"$.info.description\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)(rate.limit|429)\"\n\n  sage-oauth-authorization-code-flow:\n    description: OAuth2 security scheme must use authorizationCode flow\n    message: \"OAuth2 must use authorizationCode flow for Sage APIs\"\n    given: \"$.components.securitySchemes[*].flows\"\n    severity: warn\n    then:\n      field: authorizationCode\n      function: defined\n\n  sage-response-delete-204:\n    description: DELETE operations should return 204 No Content\n    message: \"DELETE operations should return 204 status code\"\n    given: \"$.paths[*][delete].responses\"\n    severity: info\n    then:\n      field: \"204\"\n      function:\
  \ defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sage/refs/heads/main/rules/sage-rules.yml
tags:
- Accounting
- Business Management
- Cloud Software
- ERP
- Payroll
- HR
- Spectral
- Linting
- API Governance
---
