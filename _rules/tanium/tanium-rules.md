---
api_specs:
- filename: tanium-platform-rest-api-openapi.yml
  format: yaml
  label: Tanium Platform REST API
  slug: platform-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tanium/refs/heads/main/openapi/tanium-platform-rest-api-openapi.yml
- filename: tanium-threat-response-api-openapi.yml
  format: yaml
  label: Tanium Threat Response API
  slug: threat-response-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tanium/refs/heads/main/openapi/tanium-threat-response-api-openapi.yml
- filename: tanium-connect-api-openapi.yml
  format: yaml
  label: Tanium Connect API
  slug: connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tanium/refs/heads/main/openapi/tanium-connect-api-openapi.yml
categories:
- tanium
description: Spectral linting rules defining API design standards and conventions for Tanium.
layout: rules
name: Tanium API Rules
provider_name: Tanium
provider_slug: tanium
rule_count: 8
rules:
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: tanium-operation-ids-camel-case
  severity: warn
- description: All operation summaries must use Title Case (no leading vendor prefix)
  given: $.paths[*][*].summary
  name: tanium-summary-title-case
  severity: warn
- description: API token authentication must use the session header
  given: $.components.securitySchemes[*][?(@.type == 'apiKey')]
  name: tanium-session-header-auth
  severity: info
- description: Tanium Platform API paths must be versioned under /api/v2/
  given: $.paths[*]~
  name: tanium-paths-api-versioned
  severity: hint
- description: Successful responses should use a data wrapper object
  given: $.paths[*][*].responses['200'].content['application/json'].schema
  name: tanium-responses-have-data-wrapper
  severity: hint
- description: All path and query parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: tanium-parameters-have-descriptions
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: tanium-operations-have-tags
  severity: warn
- description: 4xx/5xx responses should reference the shared Error schema
  given: $.paths[*][*].responses[?(@property >= 400)].content['application/json'].schema
  name: tanium-error-schema-consistent
  severity: warn
rules_file: rules/tanium-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tanium/refs/heads/main/rules/tanium-rules.yml
severity_counts:
  error: 0
  hint: 2
  info: 1
  warn: 5
slug: tanium-rules
source_filename: tanium-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tanium-operation-ids-camel-case:\n    description: All operationIds must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tanium-summary-title-case:\n    description: All operation summaries must use Title Case (no leading vendor prefix)\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^Tanium \"\n\n  tanium-session-header-auth:\n    description: API token authentication must use the session header\n    severity: info\n    given: \"$.components.securitySchemes[*][?(@.type == 'apiKey')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^session$\"\n\n  tanium-paths-api-versioned:\n    description: Tanium Platform API paths must be versioned under /api/v2/\n    severity: hint\n\
  \    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/api/v2/|/plugin/products/)\"\n\n  tanium-responses-have-data-wrapper:\n    description: Successful responses should use a data wrapper object\n    severity: hint\n    given: \"$.paths[*][*].responses['200'].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            data: {}\n\n  tanium-parameters-have-descriptions:\n    description: All path and query parameters must have descriptions\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tanium-operations-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tanium-error-schema-consistent:\n    description: 4xx/5xx responses should reference\
  \ the shared Error schema\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= 400)].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"$ref\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tanium/refs/heads/main/rules/tanium-rules.yml
tags:
- Compliance
- Endpoint Management
- Patch Management
- Security
- Threat Detection
- Unified Endpoint Management
- Spectral
- Linting
- API Governance
---
