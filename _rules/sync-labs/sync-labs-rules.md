---
api_specs:
- filename: sync-labs-openapi.yml
  format: yaml
  label: Sync Labs API
  slug: sync-labs-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sync-labs/refs/heads/main/openapi/sync-labs-openapi.yml
categories:
- sync
description: Spectral linting rules defining API design standards and conventions for Sync Labs.
layout: rules
name: Sync Labs API Rules
provider_name: Sync Labs
provider_slug: sync-labs
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sync-labs-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: sync-labs-operation-has-operation-id
  severity: error
- description: All operations should use API key authentication
  given: $
  name: sync-labs-api-key-auth
  severity: warn
- description: API paths should use versioned base URL (/v2/)
  given: $.servers[*].url
  name: sync-labs-v2-versioned-paths
  severity: info
- description: Async generation responses must include a status field
  given: $.components.schemas.GenerationResponse.properties
  name: sync-labs-async-status-field
  severity: warn
- description: Operations should define error responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: sync-labs-error-response-defined
  severity: warn
- description: Rate-limited endpoints should document 429 response
  given: $.paths['/generate']['post'].responses
  name: sync-labs-rate-limit-documented
  severity: warn
- description: Webhook URL parameters should use URI format
  given: $.components.schemas.*.properties.webhook_url
  name: sync-labs-webhook-url-format
  severity: hint
rules_file: rules/sync-labs-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sync-labs/refs/heads/main/rules/sync-labs-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 1
  warn: 5
slug: sync-labs-rules
source_filename: sync-labs-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  sync-labs-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /-]*$\"\n\n  sync-labs-operation-has-operation-id:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sync-labs-api-key-auth:\n    description: All operations should use API key authentication\n    message: Operations should reference ApiKeyAuth security scheme\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  sync-labs-v2-versioned-paths:\n    description: API paths should use versioned base URL (/v2/)\n\
  \    message: Operations should be under a versioned path prefix\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]$\"\n\n  sync-labs-async-status-field:\n    description: Async generation responses must include a status field\n    message: Generation response schema should include a status field\n    severity: warn\n    given: \"$.components.schemas.GenerationResponse.properties\"\n    then:\n      field: status\n      function: truthy\n\n  sync-labs-error-response-defined:\n    description: Operations should define error responses\n    message: Operation is missing error responses\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"429\"]\n\n  sync-labs-rate-limit-documented:\n\
  \    description: Rate-limited endpoints should document 429 response\n    message: POST generation endpoint should document 429 rate limit response\n    severity: warn\n    given: \"$.paths['/generate']['post'].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  sync-labs-webhook-url-format:\n    description: Webhook URL parameters should use URI format\n    message: webhook_url property should have format uri\n    severity: hint\n    given: \"$.components.schemas.*.properties.webhook_url\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - uri\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sync-labs/refs/heads/main/rules/sync-labs-rules.yml
tags:
- Artificial Intelligence
- Content Localization
- Dubbing
- Lip Sync
- Media
- Video
- Visual AI
- Spectral
- Linting
- API Governance
---
