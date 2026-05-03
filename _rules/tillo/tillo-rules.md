---
api_specs:
- filename: tillo-gift-card-openapi.yml
  format: yaml
  label: Tillo Gift Card API
  slug: tillo-gift-card-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tillo/refs/heads/main/openapi/tillo-gift-card-openapi.yml
- filename: tillo-gift-card-openapi.yml
  format: yaml
  label: Tillo Float Management API
  slug: tillo-float-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tillo/refs/heads/main/openapi/tillo-gift-card-openapi.yml
categories:
- tillo
description: Spectral linting rules defining API design standards and conventions for Tillo.
layout: rules
name: Tillo API Rules
provider_name: Tillo
provider_slug: tillo
rule_count: 7
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tillo-operation-id-camel-case
  severity: warn
- description: All paths must be part of the v2 base URL
  given: $.servers[*]
  name: tillo-versioned-paths
  severity: info
- description: All operations must have a summary
  given: $.paths[*][*]
  name: tillo-operation-summary
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: tillo-operation-tags
  severity: warn
- description: POST operations that issue or modify gift cards should include client_request_id in the request body for idempotency
  given: $.paths[*][post]
  name: tillo-client-request-id
  severity: info
- description: All successful responses should include a status field
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: tillo-status-in-response
  severity: warn
- description: API must use HMAC authentication scheme
  given: $.components.securitySchemes
  name: tillo-hmac-auth
  severity: error
rules_file: rules/tillo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tillo/refs/heads/main/rules/tillo-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 3
slug: tillo-rules
source_filename: tillo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tillo-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tillo-versioned-paths:\n    description: All paths must be part of the v2 base URL\n    message: \"Path '{{value}}' must use the /api/v2 base\"\n    severity: info\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \".*/v[0-9]+.*\"\n\n  tillo-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tillo-operation-tags:\n    description: All operations must have tags\n    message: \"Operation\
  \ must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tillo-client-request-id:\n    description: >-\n      POST operations that issue or modify gift cards should include\n      client_request_id in the request body for idempotency\n    message: \"POST operation should document client_request_id for idempotency\"\n    severity: info\n    given: \"$.paths[*][post]\"\n    then:\n      function: truthy\n\n  tillo-status-in-response:\n    description: All successful responses should include a status field\n    message: \"Response should include a 'status' field\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  tillo-hmac-auth:\n    description: API must use HMAC authentication scheme\n    message: \"API must define an HMAC authentication security\
  \ scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tillo/refs/heads/main/rules/tillo-rules.yml
tags:
- Finance
- Gift Cards
- Payments
- Rewards
- Incentives
- Spectral
- Linting
- API Governance
---
