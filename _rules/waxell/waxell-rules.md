---
api_specs:
- filename: waxell-observe-openapi.yml
  format: yaml
  label: Waxell Observe API
  slug: observe
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/waxell/refs/heads/main/openapi/waxell-observe-openapi.yml
categories:
- waxell
description: Spectral linting rules defining API design standards and conventions for Waxell.
layout: rules
name: Waxell API Rules
provider_name: Waxell
provider_slug: waxell
rule_count: 14
rules:
- description: All Waxell OpenAPI titles SHOULD start with "Waxell ".
  given: $.info.title
  name: waxell-info-title-prefix
  severity: warn
- description: All Waxell API servers MUST use HTTPS.
  given: $.servers[*].url
  name: waxell-server-https
  severity: error
- description: Waxell servers SHOULD be a tenant-specific *.waxell.dev host.
  given: $.servers[*].url
  name: waxell-server-tenant-host
  severity: warn
- description: Waxell Observe paths MUST be served under /api/v1/observe/.
  given: $.paths[*]~
  name: waxell-base-path
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: waxell-operation-id-required
  severity: error
- description: operationId SHOULD be camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: waxell-operation-id-camel-case
  severity: warn
- description: Operations MUST have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: waxell-summary-required
  severity: error
- description: Operation summaries SHOULD use Title Case.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: waxell-summary-title-case
  severity: warn
- description: Operations MUST be tagged with at least one tag.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: waxell-tags-required
  severity: warn
- description: Schema properties SHOULD use snake_case (matches the API payloads).
  given: $.components.schemas[*].properties[*]~
  name: waxell-snake-case-properties
  severity: warn
- description: Waxell paths use a trailing slash; enforce consistency.
  given: $.paths[*]~
  name: waxell-trailing-slash
  severity: warn
- description: API MUST declare a security scheme (X-Wax-Key or Bearer).
  given: $.components.securitySchemes
  name: waxell-security-required
  severity: error
- description: Error responses SHOULD reference an Error schema with `error` and `message` fields.
  given: $.components.schemas.Error.properties
  name: waxell-error-schema-shape
  severity: warn
- description: All write operations SHOULD document a 429 response for governance throttling.
  given: $.paths[*][post,put,delete,patch].responses
  name: waxell-rate-limit-response
  severity: warn
rules_file: rules/waxell-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/waxell/refs/heads/main/rules/waxell-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 9
slug: waxell-rules
source_filename: waxell-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  waxell-info-title-prefix:\n    description: All Waxell OpenAPI titles SHOULD start with \"Waxell \".\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^Waxell '\n  waxell-server-https:\n    description: All Waxell API servers MUST use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n  waxell-server-tenant-host:\n    description: Waxell servers SHOULD be a tenant-specific *.waxell.dev host.\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://(\\{tenant\\}|[a-z0-9-]+)\\.waxell\\.dev'\n  waxell-base-path:\n    description: Waxell Observe paths MUST be served under /api/v1/observe/.\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n     \
  \   match: '^/api/v1/observe/'\n  waxell-operation-id-required:\n    description: Operations MUST have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n  waxell-operation-id-camel-case:\n    description: operationId SHOULD be camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n  waxell-summary-required:\n    description: Operations MUST have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n  waxell-summary-title-case:\n    description: Operation summaries SHOULD use Title Case.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z]'\n  waxell-tags-required:\n\
  \    description: Operations MUST be tagged with at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].tags\n    then:\n      function: truthy\n  waxell-snake-case-properties:\n    description: Schema properties SHOULD use snake_case (matches the API payloads).\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n  waxell-trailing-slash:\n    description: Waxell paths use a trailing slash; enforce consistency.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '/$'\n  waxell-security-required:\n    description: API MUST declare a security scheme (X-Wax-Key or Bearer).\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n  waxell-error-schema-shape:\n    description: Error responses SHOULD reference an Error schema with `error`\
  \ and `message` fields.\n    severity: warn\n    given: $.components.schemas.Error.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [error, message]\n  waxell-rate-limit-response:\n    description: All write operations SHOULD document a 429 response for governance throttling.\n    severity: warn\n    given: $.paths[*][post,put,delete,patch].responses\n    then:\n      field: '429'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/waxell/refs/heads/main/rules/waxell-rules.yml
tags:
- AI Agent Governance
- Observability
- Policy Enforcement
- LLM Telemetry
- Cost Management
- MCP
- Agent Runtime
- Spectral
- Linting
- API Governance
---
