---
api_specs:
- filename: sportsbook-api-openapi.yml
  format: yaml
  label: Sportsbook API
  slug: sportsbook-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsbook-api/refs/heads/main/openapi/sportsbook-api-openapi.yml
categories:
- sportsbook
description: Spectral linting rules defining API design standards and conventions for Sportsbook API.
layout: rules
name: Sportsbook API API Rules
provider_name: Sportsbook API
provider_slug: sportsbook-api
rule_count: 9
rules:
- description: All operations must have exactly one tag from the approved list.
  given: $.paths[*][*]
  name: sportsbook-api-operation-tags
  severity: error
- description: All paths must be prefixed with /v1/.
  given: $.paths
  name: sportsbook-api-v1-prefix
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: sportsbook-api-operation-ids-camel-case
  severity: error
- description: All GET operations must define a 200 response.
  given: $.paths[*].get
  name: sportsbook-api-get-response-200
  severity: error
- description: API must use X-RapidAPI-Key header authentication.
  given: $.components.securitySchemes
  name: sportsbook-api-rapidapi-auth
  severity: error
- description: Sport query parameter should use enum values.
  given: $.paths[*][*].parameters[?(@.name == 'sport')].schema
  name: sportsbook-api-sport-param-enum
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sportsbook-api-summary-title-case
  severity: warn
- description: All operations should define a 401 Unauthorized response.
  given: $.paths[*][*]
  name: sportsbook-api-401-response
  severity: warn
- description: Operations that may be rate-limited should document 429 response.
  given: $.paths[*].get
  name: sportsbook-api-429-rate-limit
  severity: warn
rules_file: rules/sportsbook-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sportsbook-api/refs/heads/main/rules/sportsbook-api-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: sportsbook-api-rules
source_filename: sportsbook-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sportsbook API-specific conventions\n\n  sportsbook-api-operation-tags:\n    description: All operations must have exactly one tag from the approved list.\n    message: \"Operation must include a valid tag (Odds, Betting Analysis, Reference).\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n          maxItems: 1\n          items:\n            type: string\n            enum:\n              - Odds\n              - Betting Analysis\n              - Reference\n\n  sportsbook-api-v1-prefix:\n    description: All paths must be prefixed with /v1/.\n    message: \"Path '{{property}}' must be prefixed with /v1/.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v1\\\\/\"\n\n  sportsbook-api-operation-ids-camel-case:\n    description:\
  \ OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sportsbook-api-get-response-200:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  sportsbook-api-rapidapi-auth:\n    description: API must use X-RapidAPI-Key header authentication.\n    message: \"API must define rapidApiKey security scheme with X-RapidAPI-Key header.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: rapidApiKey\n      function: truthy\n\n  sportsbook-api-sport-param-enum:\n    description: Sport query parameter should use enum values.\n    message: \"Sport parameter should\
  \ define enum values.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'sport')].schema\"\n    then:\n      field: enum\n      function: truthy\n\n  sportsbook-api-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  sportsbook-api-401-response:\n    description: All operations should define a 401 Unauthorized response.\n    message: \"Operation should define a 401 response for unauthorized access.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  sportsbook-api-429-rate-limit:\n    description: Operations that may be rate-limited should document 429 response.\n    message: \"Operation should define a 429 response for rate limiting.\"\
  \n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.429\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sportsbook-api/refs/heads/main/rules/sportsbook-api-rules.yml
tags:
- Sports Betting
- Odds
- Sports Data
- Gambling
- Spectral
- Linting
- API Governance
---
