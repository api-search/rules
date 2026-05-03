---
api_specs:
- filename: the-odds-api-openapi.yml
  format: yaml
  label: The Odds API
  slug: the-odds-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-odds-api/refs/heads/main/openapi/the-odds-api-openapi.yml
categories:
- odds
description: Spectral linting rules defining API design standards and conventions for The Odds API.
layout: rules
name: The Odds API API Rules
provider_name: The Odds API
provider_slug: the-odds-api
rule_count: 10
rules:
- description: All Odds API operations must require the apiKey parameter.
  given: $.paths.*.*.parameters
  name: odds-api-key-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: odds-api-summary-title-case
  severity: warn
- description: All Odds API operations must have a summary.
  given: $.paths.*.*
  name: odds-api-summary-exists
  severity: error
- description: All operations must have at least one tag.
  given: $.paths.*.*
  name: odds-api-tags-exist
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths.*.*.responses
  name: odds-api-response-200
  severity: error
- description: Operations should define a 401 Unauthorized response for API key errors.
  given: $.paths.*.*.responses
  name: odds-api-response-401
  severity: warn
- description: Server URLs should use HTTPS.
  given: $.servers[*].url
  name: odds-api-server-https
  severity: warn
- description: Path parameters must have descriptions.
  given: $.paths.*.*.parameters[*]
  name: odds-api-path-param-descriptions
  severity: warn
- description: operationId should use camelCase.
  given: $.paths.*.*.operationId
  name: odds-api-operation-id-camel-case
  severity: hint
- description: 200 responses should return application/json.
  given: $.paths.*.*.responses.200.content
  name: odds-api-json-response
  severity: warn
rules_file: rules/the-odds-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-odds-api/refs/heads/main/rules/the-odds-api-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: the-odds-api-rules
source_filename: the-odds-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # API key must be required on all operations\n  odds-api-key-required:\n    description: All Odds API operations must require the apiKey parameter.\n    message: \"Operation must include the apiKey query parameter.\"\n    severity: error\n    given: \"$.paths.*.*.parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: apiKey\n\n  # Summaries must use Title Case\n  odds-api-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary should begin with a capital letter.\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations must have summaries\n  odds-api-summary-exists:\n    description: All Odds API operations must have\
  \ a summary.\n    message: \"Operation is missing a summary.\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: summary\n\n  # All operations must have tags\n  odds-api-tags-exist:\n    description: All operations must have at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: tags\n\n  # 200 responses required\n  odds-api-response-200:\n    description: All operations must define a 200 response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths.*.*.responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  # 401 response required (api key protected)\n  odds-api-response-401:\n    description: Operations should define a 401 Unauthorized response for API key errors.\n    message: \"Consider defining a 401 response.\"\n    severity: warn\n    given: \"$.paths.*.*.responses\"\
  \n    then:\n      function: truthy\n      field: \"401\"\n\n  # Server should use HTTPS\n  odds-api-server-https:\n    description: Server URLs should use HTTPS.\n    message: \"Server URL should use HTTPS.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Path parameters must be described\n  odds-api-path-param-descriptions:\n    description: Path parameters must have descriptions.\n    message: \"Parameter is missing a description.\"\n    severity: warn\n    given: \"$.paths.*.*.parameters[*]\"\n    then:\n      function: truthy\n      field: description\n\n  # OperationId must be camelCase\n  odds-api-operation-id-camel-case:\n    description: operationId should use camelCase.\n    message: \"operationId '{{value}}' should use camelCase.\"\n    severity: hint\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\
  \n\n  # Responses should include application/json\n  odds-api-json-response:\n    description: 200 responses should return application/json.\n    message: \"200 response should include application/json content type.\"\n    severity: warn\n    given: \"$.paths.*.*.responses.200.content\"\n    then:\n      function: truthy\n      field: \"application/json\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-odds-api/refs/heads/main/rules/the-odds-api-rules.yml
tags:
- Betting
- Odds
- Sports
- Scores
- Historical Data
- Spectral
- Linting
- API Governance
---
