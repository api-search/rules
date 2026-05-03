---
api_specs:
- filename: squarespace-commerce-api-openapi.yml
  format: yaml
  label: Squarespace Commerce API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-commerce-api-openapi.yml
- filename: squarespace-orders-api-openapi.yml
  format: yaml
  label: Squarespace Orders API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-orders-api-openapi.yml
- filename: squarespace-products-api-openapi.yml
  format: yaml
  label: Squarespace Products API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-products-api-openapi.yml
- filename: squarespace-inventory-api-openapi.yml
  format: yaml
  label: Squarespace Inventory API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-inventory-api-openapi.yml
- filename: squarespace-profiles-api-openapi.yml
  format: yaml
  label: Squarespace Profiles API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-profiles-api-openapi.yml
- filename: squarespace-transactions-api-openapi.yml
  format: yaml
  label: Squarespace Transactions API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-transactions-api-openapi.yml
- filename: squarespace-webhook-subscriptions-api-openapi.yml
  format: yaml
  label: Squarespace Webhook Subscriptions API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-webhook-subscriptions-api-openapi.yml
categories:
- squarespace
description: Spectral linting rules defining API design standards and conventions for Squarespace.
layout: rules
name: Squarespace API Rules
provider_name: Squarespace
provider_slug: squarespace
rule_count: 12
rules:
- description: List (GET collection) endpoints must support cursor-based pagination
  given: $.paths[?(!@property.match(/\{[^}]+\}$/))].get
  name: squarespace-list-endpoint-cursor
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: squarespace-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: squarespace-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: squarespace-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: squarespace-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: squarespace-operation-description-required
  severity: warn
- description: All operations must have tags
  given: $.paths[*][*]
  name: squarespace-operation-tags-required
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: squarespace-tags-title-case
  severity: warn
- description: Squarespace Commerce API paths should start with /commerce
  given: $.paths
  name: squarespace-paths-commerce-prefix
  severity: info
- description: Squarespace APIs use Bearer token authentication
  given: $.components.securitySchemes
  name: squarespace-bearer-auth
  severity: error
- description: Secured endpoints should document 401 Unauthorized responses
  given: $.paths[*][*].responses
  name: squarespace-401-response
  severity: warn
- description: Success responses must use application/json content type
  given: $.paths[*][*].responses['200'].content
  name: squarespace-json-response-content-type
  severity: error
rules_file: rules/squarespace-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/rules/squarespace-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 7
slug: squarespace-rules
source_filename: squarespace-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Squarespace APIs use cursor-based pagination — enforce cursor parameter on list endpoints\n  squarespace-list-endpoint-cursor:\n    description: List (GET collection) endpoints must support cursor-based pagination\n    message: GET collection endpoint is missing cursor parameter for pagination\n    severity: warn\n    given: $.paths[?(!@property.match(/\\{[^}]+\\}$/))].get\n    then:\n      field: parameters\n      function: defined\n\n  # All operations require operationId\n  squarespace-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: defined\n\n  # Operation IDs should use camelCase\n  squarespace-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: 'Operation ID \"{{value}}\" should be camelCase'\n    severity: warn\n    given:\
  \ $.paths[*][*].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  # All operations must have summaries\n  squarespace-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing summary\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: summary\n      function: defined\n\n  # Summaries must use Title Case\n  squarespace-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: 'Summary \"{{value}}\" should use Title Case'\n    severity: warn\n    given: $.paths[*][*].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(\\s[A-Z][a-zA-Z0-9]*)*$'\n\n  # All operations must have descriptions\n  squarespace-operation-description-required:\n    description: All operations must have a description\n    message: Operation is missing description\n    severity: warn\n    given:\
  \ $.paths[*][*]\n    then:\n      field: description\n      function: defined\n\n  # All operations should have tags\n  squarespace-operation-tags-required:\n    description: All operations must have tags\n    message: Operation is missing tags\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: defined\n\n  # Tags must use Title Case\n  squarespace-tags-title-case:\n    description: All tags must use Title Case\n    message: 'Tag \"{{value}}\" should use Title Case'\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(\\s[A-Z][a-zA-Z0-9]*)*$'\n\n  # API paths must start with /commerce\n  squarespace-paths-commerce-prefix:\n    description: Squarespace Commerce API paths should start with /commerce\n    message: 'Path \"{{path}}\" should begin with /commerce'\n    severity: info\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n\
  \      functionOptions:\n        match: '^\\/commerce\\/'\n\n  # Bearer auth must be used\n  squarespace-bearer-auth:\n    description: Squarespace APIs use Bearer token authentication\n    message: API must define bearerAuth security scheme\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      field: bearerAuth\n      function: defined\n\n  # 401 unauthorized should be defined for secured endpoints\n  squarespace-401-response:\n    description: Secured endpoints should document 401 Unauthorized responses\n    message: Secured endpoint is missing 401 response\n    severity: warn\n    given: $.paths[*][*].responses\n    then:\n      field: '401'\n      function: defined\n\n  # JSON responses should use application/json content type\n  squarespace-json-response-content-type:\n    description: Success responses must use application/json content type\n    message: 200 response must return application/json\n    severity: error\n    given: $.paths[*][*].responses['200'].content\n\
  \    then:\n      field: 'application/json'\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/rules/squarespace-rules.yml
tags:
- Commerce
- E-Commerce
- Marketing
- Payments
- Retail
- Website Builder
- Webhooks
- Spectral
- Linting
- API Governance
---
