---
api_specs:
- filename: vizion-container-tracking-openapi.yml
  format: yaml
  label: Vizion Container Tracking API
  slug: container-tracking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vizion/refs/heads/main/openapi/vizion-container-tracking-openapi.yml
categories:
- vizion
description: Spectral linting rules defining API design standards and conventions for Vizion.
layout: rules
name: Vizion API Rules
provider_name: Vizion
provider_slug: vizion
rule_count: 8
rules:
- description: Operation IDs must use camelCase to match Vizion SDK conventions.
  given: $.paths[*][*].operationId
  name: vizion-operation-ids-camel-case
  severity: warn
- description: All Vizion API operations require X-API-Key authentication.
  given: $.paths[*][*]
  name: vizion-require-api-key-security
  severity: error
- description: All operations must have a human-readable summary.
  given: $.paths[*][*]
  name: vizion-require-summaries
  severity: error
- description: All operations and schemas must have descriptions.
  given:
  - $.paths[*][*]
  - $.components.schemas[*]
  name: vizion-require-descriptions
  severity: warn
- description: All path parameters must be described.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: vizion-path-params-have-descriptions
  severity: warn
- description: All protected operations should define a 401 Unauthorized response.
  given: $.paths[*][*]
  name: vizion-responses-define-401
  severity: warn
- description: All date/time fields must use ISO 8601 format (format = date-time).
  given: $.components.schemas[*].properties[*][?(@.type == 'string')]
  name: vizion-use-iso8601-dates
  severity: warn
- description: OpenAPI specs must define at least one server.
  given: $
  name: vizion-require-server
  severity: error
rules_file: rules/vizion-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vizion/refs/heads/main/rules/vizion-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: vizion-rules
source_filename: vizion-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  vizion-operation-ids-camel-case:\n    description: Operation IDs must use camelCase to match Vizion SDK conventions.\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vizion-require-api-key-security:\n    description: All Vizion API operations require X-API-Key authentication.\n    message: \"Operation {{path}} must define security with ApiKeyAuth\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  vizion-require-summaries:\n    description: All operations must have a human-readable summary.\n    message: \"Operation {{path}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  vizion-require-descriptions:\n    description: All\
  \ operations and schemas must have descriptions.\n    message: \"{{path}} must have a description\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  vizion-path-params-have-descriptions:\n    description: All path parameters must be described.\n    message: \"Path parameter {{path}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  vizion-responses-define-401:\n    description: All protected operations should define a 401 Unauthorized response.\n    message: \"Authenticated operation {{path}} should define a 401 response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  vizion-use-iso8601-dates:\n    description: All date/time fields must use ISO 8601 format (format = date-time).\n    message:\
  \ \"Date field {{path}} must use format: date-time\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*][?(@.type == 'string')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              description:\n                pattern: \"(date|time|timestamp|created|updated|departed|arrived)\"\n          then:\n            required: [\"format\"]\n\n  vizion-require-server:\n    description: OpenAPI specs must define at least one server.\n    message: \"Spec must define at least one server\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vizion/refs/heads/main/rules/vizion-rules.yml
tags:
- Container Tracking
- Logistics
- Ocean Freight
- Shipping
- Supply Chain
- Webhooks
- Spectral
- Linting
- API Governance
---
