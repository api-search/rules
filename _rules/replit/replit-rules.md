---
api_specs:
- filename: replit-openapi.yml
  format: yaml
  label: Replit
  slug: replit
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/replit/refs/heads/main/openapi/replit-openapi.yml
categories:
- replit
description: Spectral linting rules defining API design standards and conventions for Replit.
layout: rules
name: Replit API Rules
provider_name: Replit
provider_slug: replit
rule_count: 8
rules:
- description: Replit operationIds must use dot-notation
  given: $.paths.*.*
  name: replit-operation-id-dot-notation
  severity: warn
- description: All Replit operations must have an operationId
  given: $.paths.*[get,post,put,patch,delete]
  name: replit-operation-id-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths.*.*
  name: replit-summary-title-case
  severity: warn
- description: Replit API uses Bearer token authentication
  given: $.components.securitySchemes.*
  name: replit-bearer-auth
  severity: error
- description: List responses must use items/nextCursor pagination envelope
  given: $.paths.*[get][responses][200][content][application/json][schema][properties]
  name: replit-paginated-list-response
  severity: hint
- description: DELETE operations must return 204
  given: $.paths.*[delete][responses]
  name: replit-delete-returns-204
  severity: warn
- description: Path parameters must use camelCase
  given: $.paths.*.*[parameters][?(@.in == 'path')]
  name: replit-path-camel-case-params
  severity: warn
- description: All tags must use Title Case
  given: $.paths.*.*.tags.*
  name: replit-tags-title-case
  severity: warn
rules_file: rules/replit-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/replit/refs/heads/main/rules/replit-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 5
slug: replit-rules
source_filename: replit-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Replit API conventions:\n  # - Bearer token auth\n  # - Paginated list responses use {items, nextCursor} envelope\n  # - Dot-notation operationIds (e.g. repls.list, repls.deployments.create)\n  # - Path parameters use camelCase (replId, deploymentId, username)\n  # - PATCH for partial updates, DELETE returns 204\n\n  replit-operation-id-dot-notation:\n    description: Replit operationIds must use dot-notation\n    message: \"OperationId '{{value}}' must use dot-notation like 'resource.action'\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9]*(?:\\\\.[a-z][a-z0-9]*)+$\"\n\n  replit-operation-id-required:\n    description: All Replit operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field:\
  \ operationId\n      function: truthy\n\n  replit-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: summary\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  replit-bearer-auth:\n    description: Replit API uses Bearer token authentication\n    message: \"Security scheme must be http/bearer\"\n    severity: error\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  replit-paginated-list-response:\n    description: List responses must use items/nextCursor pagination envelope\n    message: \"List responses should use 'items' array and 'nextCursor' pagination\"\n    severity: hint\n    given: \"$.paths.*[get][responses][200][content][application/json][schema][properties]\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              items:\n                type: object\n          then:\n            required:\n              - items\n\n  replit-delete-returns-204:\n    description: DELETE operations must return 204\n    message: \"DELETE operations should return a 204 No Content response\"\n    severity: warn\n    given: \"$.paths.*[delete][responses]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"204\"]\n\n  replit-path-camel-case-params:\n    description: Path parameters must use camelCase\n    message: \"Path parameter '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths.*.*[parameters][?(@.in == 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  replit-tags-title-case:\n    description: All tags must use Title Case\n    message:\
  \ \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*.tags.*\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/replit/refs/heads/main/rules/replit-rules.yml
tags:
- Code
- Compiling
- Development Environment
- Programming Languages
- Version Control
- Spectral
- Linting
- API Governance
---
