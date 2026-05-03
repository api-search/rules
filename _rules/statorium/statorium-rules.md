---
api_specs:
- filename: statorium-football-api-openapi.yml
  format: yaml
  label: Statorium Football API
  slug: football-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statorium/refs/heads/main/openapi/statorium-football-api-openapi.yml
- filename: statorium-basketball-api-openapi.yml
  format: yaml
  label: Statorium Basketball API
  slug: basketball-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statorium/refs/heads/main/openapi/statorium-basketball-api-openapi.yml
- filename: statorium-american-football-api-openapi.yml
  format: yaml
  label: Statorium American Football API
  slug: american-football-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statorium/refs/heads/main/openapi/statorium-american-football-api-openapi.yml
categories:
- statorium
description: Spectral linting rules defining API design standards and conventions for Statorium.
layout: rules
name: Statorium API Rules
provider_name: Statorium
provider_slug: statorium
rule_count: 8
rules:
- description: Statorium APIs require the API key as a query parameter named "apikey". All paths should declare this parameter requirement.
  given: $.paths[*][*]
  name: statorium-api-key-in-query
  severity: error
- description: Statorium API paths consistently use trailing slashes for collection endpoints. Paths should end with "/" for list operations.
  given: $.paths
  name: statorium-trailing-slash-paths
  severity: hint
- description: Statorium uses integer IDs for all entity identifiers (leagues, teams, players, matches). Path parameters for IDs should be typed as integer.
  given: $.paths[*][*].parameters[?(@.in == 'path')][?(@.name =~ /(leagueId|teamId|playerId|matchId|gameId)/)]
  name: statorium-integer-ids
  severity: warn
- description: Statorium API operation IDs use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: statorium-operation-ids-camel-case
  severity: warn
- description: All operation summaries in Statorium APIs must use Title Case for consistency and readability.
  given: $.paths[*][*].summary
  name: statorium-summaries-title-case
  severity: warn
- description: Every operation must have at least one tag for proper grouping and documentation in the Statorium API.
  given: $.paths[*][*]
  name: statorium-tags-defined
  severity: error
- description: Statorium API success responses should return application/json content as the primary content type.
  given: $.paths[*][*].responses['200'].content
  name: statorium-200-responses-json
  severity: warn
- description: Statorium uses consistent status values (live, scheduled, finished) for match/game status fields across all sports APIs.
  given: $.components.schemas[*].properties.status.enum
  name: statorium-status-enum-values
  severity: hint
rules_file: rules/statorium-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/statorium/refs/heads/main/rules/statorium-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 4
slug: statorium-rules
source_filename: statorium-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  statorium-api-key-in-query:\n    description: >-\n      Statorium APIs require the API key as a query parameter named \"apikey\".\n      All paths should declare this parameter requirement.\n    message: >-\n      Statorium API operations must require the \"apikey\" query parameter for\n      authentication.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            parameters:\n              type: array\n              contains:\n                type: object\n                properties:\n                  name:\n                    const: apikey\n                  in:\n                    const: query\n                  required:\n                    const: true\n\n  statorium-trailing-slash-paths:\n    description: >-\n      Statorium API paths consistently use trailing slashes for collection\n      endpoints. Paths\
  \ should end with \"/\" for list operations.\n    message: >-\n      Collection endpoints (list operations) should end with a trailing slash\n      to match the Statorium API convention.\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\/$\"\n\n  statorium-integer-ids:\n    description: >-\n      Statorium uses integer IDs for all entity identifiers (leagues, teams,\n      players, matches). Path parameters for IDs should be typed as integer.\n    message: >-\n      Path parameters named \"leagueId\", \"teamId\", \"playerId\", or \"matchId\"\n      should have type integer.\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')][?(@.name =~ /(leagueId|teamId|playerId|matchId|gameId)/)]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  statorium-operation-ids-camel-case:\n    description: >-\n      Statorium\
  \ API operation IDs use camelCase naming convention.\n    message: \"Operation IDs should use camelCase ({{value}} does not match).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  statorium-summaries-title-case:\n    description: >-\n      All operation summaries in Statorium APIs must use Title Case for\n      consistency and readability.\n    message: \"Operation summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  statorium-tags-defined:\n    description: >-\n      Every operation must have at least one tag for proper grouping and\n      documentation in the Statorium API.\n    message: \"Operations must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n\
  \      function: truthy\n\n  statorium-200-responses-json:\n    description: >-\n      Statorium API success responses should return application/json content\n      as the primary content type.\n    message: \"Success responses should include application/json content.\"\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content\"\n    then:\n      function: truthy\n\n  statorium-status-enum-values:\n    description: >-\n      Statorium uses consistent status values (live, scheduled, finished)\n      for match/game status fields across all sports APIs.\n    message: >-\n      Status fields should use the standard Statorium status values:\n      live, scheduled, finished.\n    severity: hint\n    given: \"$.components.schemas[*].properties.status.enum\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          items:\n            type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/statorium/refs/heads/main/rules/statorium-rules.yml
tags:
- Sports
- Sports Data
- Football
- Soccer
- Basketball
- American Football
- Live Scores
- Statistics
- Spectral
- Linting
- API Governance
---
