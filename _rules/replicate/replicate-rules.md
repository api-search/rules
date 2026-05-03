---
api_specs:
- filename: replicate-openapi.yml
  format: yaml
  label: Replicate
  slug: replicate
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/replicate/refs/heads/main/openapi/replicate-openapi.yml
categories:
- replicate
description: Spectral linting rules defining API design standards and conventions for Replicate.
layout: rules
name: Replicate API Rules
provider_name: Replicate
provider_slug: replicate
rule_count: 10
rules:
- description: Replicate operationIds must use dot-notation (e.g. predictions.create, models.versions.list)
  given: $.paths.*.*
  name: replicate-operation-id-dot-notation
  severity: warn
- description: All Replicate operations must have an operationId
  given: $.paths.*[get,post,put,patch,delete]
  name: replicate-operation-id-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths.*.*
  name: replicate-summary-title-case
  severity: warn
- description: Replicate API uses Bearer token authentication
  given: $.components.securitySchemes.*
  name: replicate-bearer-auth
  severity: error
- description: List operations should return a paginated response with next, previous, and results fields
  given: $.paths.*[get][responses][200][content][application/json][schema][properties]
  name: replicate-paginated-list-response
  severity: hint
- description: Path segments must use kebab-case or be path parameters
  given: $.paths
  name: replicate-path-kebab-case
  severity: warn
- description: Operations must define at least one 200 or 204 response
  given: $.paths.*[get,post,put,patch,delete][responses]
  name: replicate-200-or-204-response
  severity: warn
- description: All tags must use Title Case
  given: $.paths.*.*.tags.*
  name: replicate-tags-title-case
  severity: warn
- description: Version ID parameters must be string type
  given: $.paths.*.*[parameters][?(@.name == 'version_id')]
  name: replicate-version-id-string
  severity: warn
- description: Cancel operations must follow the /cancel path convention
  given: $.paths
  name: replicate-cancel-path-convention
  severity: hint
rules_file: rules/replicate-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/replicate/refs/heads/main/rules/replicate-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 6
slug: replicate-rules
source_filename: replicate-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Replicate API conventions:\n  # - All paths use kebab-case with dot-separated operationIds (e.g. account.get, models.versions.list)\n  # - Bearer auth via Authorization header\n  # - Paginated list responses use {next, previous, results} envelope\n  # - Predictions and Trainings follow same lifecycle (create, get, cancel)\n  # - Version IDs are opaque strings\n  # - Webhook support for async operations\n\n  replicate-operation-id-dot-notation:\n    description: Replicate operationIds must use dot-notation (e.g. predictions.create, models.versions.list)\n    message: \"OperationId '{{value}}' must use dot-notation like 'resource.action' or 'resource.subresource.action'\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9]*(?:\\\\.[a-z][a-z0-9]*)+$\"\n\n  replicate-operation-id-required:\n    description: All Replicate operations\
  \ must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  replicate-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: summary\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  replicate-bearer-auth:\n    description: Replicate API uses Bearer token authentication\n    message: \"Security scheme must be of type 'http' with scheme 'bearer'\"\n    severity: error\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  replicate-paginated-list-response:\n \
  \   description: List operations should return a paginated response with next, previous, and results fields\n    message: \"List operations should include 'next', 'previous', and 'results' fields in response schema\"\n    severity: hint\n    given: \"$.paths.*[get][responses][200][content][application/json][schema][properties]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              results:\n                type: object\n          then:\n            required:\n              - next\n              - previous\n              - results\n\n  replicate-path-kebab-case:\n    description: Path segments must use kebab-case or be path parameters\n    message: \"Path segment '{{value}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-z_]+\\\\}))+$\"\n\n  replicate-200-or-204-response:\n\
  \    description: Operations must define at least one 200 or 204 response\n    message: \"Operation must define a 200 or 204 success response\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete][responses]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"204\"]\n\n  replicate-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*.tags.*\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  replicate-version-id-string:\n    description: Version ID parameters must be string type\n    message: \"Version ID path parameter must be of type string\"\n    severity: warn\n    given: \"$.paths.*.*[parameters][?(@.name == 'version_id')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n\
  \        values:\n          - string\n\n  replicate-cancel-path-convention:\n    description: Cancel operations must follow the /cancel path convention\n    message: \"Cancel operation path must end with '/cancel'\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            pattern: cancel\n          then:\n            pattern: \".*\\\\/cancel$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/replicate/refs/heads/main/rules/replicate-rules.yml
tags:
- Artificial Intelligence
- Machine Learning
- Image Generation
- Language Models
- Model Deployment
- Spectral
- Linting
- API Governance
---
