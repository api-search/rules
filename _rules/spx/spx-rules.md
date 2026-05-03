---
api_specs:
- filename: spx-graphics-control-api-openapi.yml
  format: yaml
  label: SPX Graphics Control API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spx/refs/heads/main/openapi/spx-graphics-control-api-openapi.yml
categories:
- spx
description: Spectral linting rules defining API design standards and conventions for SPX Graphics.
layout: rules
name: SPX Graphics API Rules
provider_name: SPX Graphics
provider_slug: spx
rule_count: 8
rules:
- description: Operation IDs should follow verbNoun camelCase convention
  given: $.paths[*][*].operationId
  name: spx-operation-id-verb-noun
  severity: warn
- description: All SPX API paths must be under /api/v1
  given: $.paths
  name: spx-paths-versioned
  severity: error
- description: All operations should have a summary
  given: $.paths[*][*]
  name: spx-operation-summary-required
  severity: warn
- description: All operations should have at least one tag
  given: $.paths[*][*]
  name: spx-operation-tags-required
  severity: warn
- description: The API key query parameter must be named 'apikey'
  given: $.paths[*][*].parameters[*]
  name: spx-apikey-parameter-name
  severity: warn
- description: Operations must define a 200 success response
  given: $.paths[*][*].responses
  name: spx-success-response-required
  severity: error
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spx-tags-title-case
  severity: warn
- description: POST operations must define a request body content type
  given: $.paths[*].post
  name: spx-post-content-type
  severity: warn
rules_file: rules/spx-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spx/refs/heads/main/rules/spx-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: spx-rules
source_filename: spx-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SPX Graphics API uses GET for most commands — operations must be named with verb-noun\n  spx-operation-id-verb-noun:\n    description: Operation IDs should follow verbNoun camelCase convention\n    message: 'Operation ID \"{{value}}\" should be verbNoun camelCase (e.g., playItem, loadRundown)'\n    severity: warn\n    given: $.paths[*][*].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  # All paths must be under /api/v1\n  spx-paths-versioned:\n    description: All SPX API paths must be under /api/v1\n    message: 'Path \"{{path}}\" must start with /api/v1'\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^\\/api\\/v1\\/'\n\n  # Operations should have summaries\n  spx-operation-summary-required:\n    description: All operations should have a summary\n    message: Operation is missing a\
  \ summary\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: summary\n      function: defined\n\n  # Operations should have tags\n  spx-operation-tags-required:\n    description: All operations should have at least one tag\n    message: Operation is missing tags\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: defined\n\n  # API key parameter should be named 'apikey'\n  spx-apikey-parameter-name:\n    description: The API key query parameter must be named 'apikey'\n    message: 'Query parameter for authentication should be named \"apikey\", found \"{{value}}\"'\n    severity: warn\n    given: $.paths[*][*].parameters[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              in:\n                const: query\n              description:\n                pattern: API key\n          then:\n            properties:\n              name:\n                const:\
  \ apikey\n\n  # Responses must include 200\n  spx-success-response-required:\n    description: Operations must define a 200 success response\n    message: Operation is missing a 200 response\n    severity: error\n    given: $.paths[*][*].responses\n    then:\n      field: '200'\n      function: defined\n\n  # Tags must use Title Case\n  spx-tags-title-case:\n    description: All tags must use Title Case\n    message: 'Tag \"{{value}}\" should use Title Case'\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(\\s[A-Z][a-zA-Z0-9]*)*$'\n\n  # Request bodies for POST endpoints should define content type\n  spx-post-content-type:\n    description: POST operations must define a request body content type\n    message: POST operation is missing requestBody content definition\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spx/refs/heads/main/rules/spx-rules.yml
tags:
- Broadcast
- Graphics
- Live Production
- Media
- Streaming
- Video Production
- Spectral
- Linting
- API Governance
---
