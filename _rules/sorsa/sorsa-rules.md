---
api_specs:
- filename: sorsa-openapi.yml
  format: yaml
  label: Sorsa API v3
  slug: sorsa-api-v3
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sorsa/refs/heads/main/openapi/sorsa-openapi.yml
categories:
- sorsa
description: Spectral linting rules defining API design standards and conventions for Sorsa.
layout: rules
name: Sorsa API Rules
provider_name: Sorsa
provider_slug: sorsa
rule_count: 8
rules:
- description: Paths must be lowercase kebab-case (e.g. /tweet-info, /check-follow). Underscores and camelCase are not permitted.
  given: $.paths.*~
  name: sorsa-paths-are-lowercase-kebab
  severity: error
- description: Every operation must declare a human-readable summary in Title Case.
  given: $.paths.*[get,post,put,delete,patch]
  name: sorsa-operations-have-summary
  severity: error
- description: Every operation must declare at least one tag drawn from the canonical tag taxonomy.
  given: $.paths.*[get,post,put,delete,patch]
  name: sorsa-operations-have-tags
  severity: error
- description: Every operation should declare a stable operationId for SDK generation.
  given: $.paths.*[get,post,put,delete,patch]
  name: sorsa-operations-have-operationId
  severity: warn
- description: Sorsa uses a single `ApiKey` header. The OpenAPI spec must declare exactly that security scheme.
  given: $.components.securitySchemes.ApiKey
  name: sorsa-auth-is-apikey-header
  severity: error
- description: The spec must declare https://api.sorsa.io/v3 as a server.
  given: $.servers[*].url
  name: sorsa-uses-canonical-server
  severity: error
- description: Operations should document at minimum 400, 401, 429 responses.
  given: $.paths.*[get,post,put,delete,patch].responses
  name: sorsa-error-responses-defined
  severity: warn
- description: Paginated list responses should expose a `next_cursor` field (Sorsa convention).
  given: $.components.schemas[?(@property.match(/.*Response$/i))].properties
  name: sorsa-pagination-uses-next-cursor
  severity: hint
rules_file: rules/sorsa-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sorsa/refs/heads/main/rules/sorsa-rules.yml
severity_counts:
  error: 5
  hint: 1
  info: 0
  warn: 2
slug: sorsa-rules
source_filename: sorsa-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\noverrides: []\nrules:\n  # Sorsa-specific conventions inferred from the v3 OpenAPI spec\n  sorsa-paths-are-lowercase-kebab:\n    description: Paths must be lowercase kebab-case (e.g. /tweet-info, /check-follow). Underscores and camelCase are not permitted.\n    message: \"Path {{value}} must be lowercase kebab-case (only [a-z0-9-/{}] characters).\"\n    given: $.paths.*~\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9-]+(/\\\\{[a-z_]+\\\\}|/[a-z0-9-]+)*$\"\n\n  sorsa-operations-have-summary:\n    description: Every operation must declare a human-readable summary in Title Case.\n    message: \"Operation {{path}} is missing a summary.\"\n    given: $.paths.*[get,post,put,delete,patch]\n    severity: error\n    then:\n      field: summary\n      function: truthy\n\n  sorsa-operations-have-tags:\n    description: Every operation must declare at least one tag drawn from the canonical tag taxonomy.\n\
  \    given: $.paths.*[get,post,put,delete,patch]\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  sorsa-operations-have-operationId:\n    description: Every operation should declare a stable operationId for SDK generation.\n    given: $.paths.*[get,post,put,delete,patch]\n    severity: warn\n    then:\n      field: operationId\n      function: truthy\n\n  sorsa-auth-is-apikey-header:\n    description: Sorsa uses a single `ApiKey` header. The OpenAPI spec must declare exactly that security scheme.\n    given: $.components.securitySchemes.ApiKey\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [type, in, name]\n          properties:\n            type: { const: apiKey }\n            in: { const: header }\n            name: { const: ApiKey }\n\n  sorsa-uses-canonical-server:\n    description: The spec must declare https://api.sorsa.io/v3 as a server.\n    given: $.servers[*].url\n\
  \    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.sorsa\\\\.io/v3$\"\n\n  sorsa-error-responses-defined:\n    description: Operations should document at minimum 400, 401, 429 responses.\n    given: $.paths.*[get,post,put,delete,patch].responses\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"429\"]\n\n  sorsa-pagination-uses-next-cursor:\n    description: Paginated list responses should expose a `next_cursor` field (Sorsa convention).\n    message: \"List responses should use `next_cursor` for pagination.\"\n    given: $.components.schemas[?(@property.match(/.*Response$/i))].properties\n    severity: hint\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sorsa/refs/heads/main/rules/sorsa-rules.yml
tags:
- Twitter
- X
- Social Media
- Data Extraction
- Real-Time
- Spectral
- Linting
- API Governance
---
