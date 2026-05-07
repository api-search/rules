---
api_specs:
- filename: openapi.json
  format: json
  label: KonbiniAPI Main Spec
  slug: main
  spec_type: OpenAPI
  url: https://docs.konbiniapi.com/openapi.json
categories:
- konbiniapi
description: Spectral linting rules defining API design standards and conventions for KonbiniAPI.
layout: rules
name: KonbiniAPI API Rules
provider_name: KonbiniAPI
provider_slug: konbiniapi
rule_count: 10
rules:
- description: All paths must be prefixed with /v1/ for KonbiniAPI versioning.
  given: $.paths
  name: konbiniapi-paths-must-be-versioned
  severity: error
- description: All paths must include the platform segment (instagram or tiktok).
  given: $.paths
  name: konbiniapi-paths-must-include-platform
  severity: error
- description: KonbiniAPI is a read-only data layer. Only GET operations are supported.
  given: $.paths.*
  name: konbiniapi-operations-must-be-get
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.get.summary
  name: konbiniapi-operation-summary-title-case
  severity: warn
- description: Every operation must have an operationId in camelCase.
  given: $.paths.*.get
  name: konbiniapi-operation-must-have-operationid
  severity: error
- description: Successful responses must declare X-Credits-Remaining and X-Credits-Used headers.
  given: $.paths.*.get.responses["200"]
  name: konbiniapi-response-must-include-credit-headers
  severity: warn
- description: Global security must use a Bearer (HTTP) scheme.
  given: $.components.securitySchemes
  name: konbiniapi-must-use-bearer-auth
  severity: error
- description: All servers must use HTTPS.
  given: $.servers[*].url
  name: konbiniapi-server-must-be-https
  severity: error
- description: Component schema names must use PascalCase.
  given: $.components.schemas
  name: konbiniapi-schemas-pascal-case
  severity: warn
- description: Every operation must be tagged with Instagram or TikTok.
  given: $.paths.*.get.tags
  name: konbiniapi-must-tag-operations
  severity: error
rules_file: rules/konbiniapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/konbiniapi/refs/heads/main/rules/konbiniapi-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 3
slug: konbiniapi-rules
source_filename: konbiniapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\ndocumentationUrl: https://docs.konbiniapi.com\nfunctions: []\nrules:\n  # KonbiniAPI conventions: derived from konbiniapi-openapi.yml\n  konbiniapi-paths-must-be-versioned:\n    description: All paths must be prefixed with /v1/ for KonbiniAPI versioning.\n    message: 'Path \"{{property}}\" must start with /v1/.'\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^/v1/'\n\n  konbiniapi-paths-must-include-platform:\n    description: All paths must include the platform segment (instagram or tiktok).\n    message: 'Path \"{{property}}\" must include /tiktok/ or /instagram/.'\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^/v1/(tiktok|instagram)/'\n\n  konbiniapi-operations-must-be-get:\n    description: KonbiniAPI is a read-only data layer. Only GET operations are supported.\n\
  \    message: '{{path}} uses {{property}}; KonbiniAPI only supports GET.'\n    severity: error\n    given: $.paths.*\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          not:\n            anyOf:\n              - required: ['post']\n              - required: ['put']\n              - required: ['patch']\n              - required: ['delete']\n\n  konbiniapi-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: 'Summary \"{{value}}\" should be Title Case.'\n    severity: warn\n    given: $.paths.*.get.summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^([A-Z0-9][A-Za-z0-9]*)( (a|an|and|the|or|but|for|with|to|of|in|on|at|by|from|as|is|vs|API|URL|MCP|HTTP|HTTPS|TikTok|Instagram|ID|IDs|HD|UHD)| [A-Z0-9][A-Za-z0-9]*)*$'\n\n  konbiniapi-operation-must-have-operationid:\n    description: Every operation must have an operationId in camelCase.\n    message: 'operationId\
  \ \"{{value}}\" must be camelCase.'\n    severity: error\n    given: $.paths.*.get\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  konbiniapi-response-must-include-credit-headers:\n    description: Successful responses must declare X-Credits-Remaining and X-Credits-Used headers.\n    message: '200 response missing credit-tracking headers.'\n    severity: warn\n    given: $.paths.*.get.responses[\"200\"]\n    then:\n      field: headers\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [X-Credits-Remaining, X-Credits-Used]\n\n  konbiniapi-must-use-bearer-auth:\n    description: Global security must use a Bearer (HTTP) scheme.\n    message: 'KonbiniAPI requires Bearer token authentication.'\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \          patternProperties:\n            '^.*$':\n              type: object\n              properties:\n                type: { const: http }\n                scheme: { const: bearer }\n\n  konbiniapi-server-must-be-https:\n    description: All servers must use HTTPS.\n    message: 'Server URL \"{{value}}\" must use HTTPS.'\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  konbiniapi-schemas-pascal-case:\n    description: Component schema names must use PascalCase.\n    message: 'Schema \"{{property}}\" must be PascalCase.'\n    severity: warn\n    given: $.components.schemas\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z0-9]+$'\n\n  konbiniapi-must-tag-operations:\n    description: Every operation must be tagged with Instagram or TikTok.\n    message: 'Operation must be tagged Instagram or TikTok.'\n    severity: error\n    given:\
  \ $.paths.*.get.tags\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n          contains:\n            enum: [Instagram, TikTok]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/konbiniapi/refs/heads/main/rules/konbiniapi-rules.yml
tags:
- API
- Social Media
- Instagram
- TikTok
- ActivityStreams 2.0
- Scraping
- Data Extraction
- Public Data
- Influencer Marketing
- Social Listening
- Creator Tools
- MCP
- Model Context Protocol
- Spectral
- Linting
- API Governance
---
