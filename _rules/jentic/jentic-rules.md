---
api_specs:
- filename: jentic-openapi.yml
  format: yaml
  label: Jentic API
  slug: jentic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/jentic/refs/heads/main/openapi/jentic-openapi.yml
categories:
- jentic
description: Spectral linting rules defining API design standards and conventions for Jentic.
layout: rules
name: Jentic API Rules
provider_name: Jentic
provider_slug: jentic
rule_count: 14
rules:
- description: API title must include "Jentic".
  given: $.info.title
  name: jentic-info-title
  severity: error
- description: API info.description is required and must be substantive.
  given: $.info
  name: jentic-info-description-required
  severity: error
- description: API must have a contact entry pointing at Jentic Support.
  given: $.info.contact
  name: jentic-info-contact-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: jentic-server-url-https
  severity: error
- description: Production server path must include the /api/v1 prefix.
  given: $.servers[?(@.description == 'Production')].url
  name: jentic-server-versioned-path
  severity: warn
- description: operationId must be camelCase.
  given: $.paths.*.*.operationId
  name: jentic-operation-id-camel-case
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: jentic-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths.*.*
  name: jentic-description-required
  severity: error
- description: Every operation must be tagged with at least one tag.
  given: $.paths.*.*.tags
  name: jentic-tags-required
  severity: error
- description: Operation tags must come from the canonical Jentic tag set.
  given: $.paths.*.*.tags[*]
  name: jentic-tag-allowed-values
  severity: warn
- description: API key auth must use the X-JENTIC-API-KEY header.
  given: $.components.securitySchemes.apiKeyAuth
  name: jentic-api-key-header
  severity: error
- description: Operation/workflow UUID fields must enforce op_/wf_ prefix.
  given: $.components.schemas..[?(@property === 'uuid')].pattern
  name: jentic-uuid-pattern
  severity: warn
- description: 4xx/5xx responses must reference ErrorResponse.
  given: $.paths.*.*.responses[?(@property.match(/^[45]/))].content.application/json.schema
  name: jentic-error-response-schema
  severity: warn
- description: ExecutionRequest.execution_type must be enum operation|workflow.
  given: $.components.schemas.ExecutionRequest.properties.execution_type.enum
  name: jentic-execution-type-enum
  severity: error
rules_file: rules/jentic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/jentic/refs/heads/main/rules/jentic-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 5
slug: jentic-rules
source_filename: jentic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\ndocumentationUrl: https://docs.jentic.com/\n\nfunctions: []\n\nrules:\n  jentic-info-title:\n    description: API title must include \"Jentic\".\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '(?i)jentic'\n\n  jentic-info-description-required:\n    description: API info.description is required and must be substantive.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  jentic-info-contact-required:\n    description: API must have a contact entry pointing at Jentic Support.\n    severity: error\n    given: $.info.contact\n    then:\n      - field: name\n        function: truthy\n      - field: url\n        function: truthy\n\n  jentic-server-url-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n       \
  \ match: '^https://'\n\n  jentic-server-versioned-path:\n    description: Production server path must include the /api/v1 prefix.\n    severity: warn\n    given: $.servers[?(@.description == 'Production')].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '/api/v1'\n\n  jentic-operation-id-camel-case:\n    description: operationId must be camelCase.\n    severity: error\n    given: $.paths.*.*.operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  jentic-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: $.paths.*.*.summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^([A-Z][a-zA-Z0-9]*)(\\s+([A-Z][a-zA-Z0-9]*|A|An|And|As|At|But|By|For|If|In|Of|On|Or|The|To|Up|Via))*$'\n\n  jentic-description-required:\n    description: Every operation must have a description.\n    severity: error\n    given: $.paths.*.*\n\
  \    then:\n      field: description\n      function: truthy\n\n  jentic-tags-required:\n    description: Every operation must be tagged with at least one tag.\n    severity: error\n    given: $.paths.*.*.tags\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  jentic-tag-allowed-values:\n    description: Operation tags must come from the canonical Jentic tag set.\n    severity: warn\n    given: $.paths.*.*.tags[*]\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Authentication\n          - Search\n          - Execution\n\n  jentic-api-key-header:\n    description: API key auth must use the X-JENTIC-API-KEY header.\n    severity: error\n    given: $.components.securitySchemes.apiKeyAuth\n    then:\n      - field: type\n        function: pattern\n        functionOptions:\n          match: '^apiKey$'\n      - field: in\n        function: pattern\n        functionOptions:\n          match: '^header$'\n      - field:\
  \ name\n        function: pattern\n        functionOptions:\n          match: '^X-JENTIC-API-KEY$'\n\n  jentic-uuid-pattern:\n    description: Operation/workflow UUID fields must enforce op_/wf_ prefix.\n    severity: warn\n    given: $.components.schemas..[?(@property === 'uuid')].pattern\n    then:\n      function: pattern\n      functionOptions:\n        match: 'op_|wf_'\n\n  jentic-error-response-schema:\n    description: 4xx/5xx responses must reference ErrorResponse.\n    severity: warn\n    given: $.paths.*.*.responses[?(@property.match(/^[45]/))].content.application/json.schema\n    then:\n      field: $ref\n      function: pattern\n      functionOptions:\n        match: 'ErrorResponse'\n\n  jentic-execution-type-enum:\n    description: ExecutionRequest.execution_type must be enum operation|workflow.\n    severity: error\n    given: $.components.schemas.ExecutionRequest.properties.execution_type.enum\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          type: array\n          items:\n            type: string\n            enum: [operation, workflow]\n          minItems: 2\n          maxItems: 2\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/jentic/refs/heads/main/rules/jentic-rules.yml
tags:
- AI Agents
- Arazzo
- OpenAPI
- MCP
- Workflows
- Integrations
- Agent Runtime
- Standard Agent
- Just In Time Tooling
- Credential Vault
- Agent Governance
- Observability
- API AI Readiness
- Spectral
- Linting
- API Governance
---
