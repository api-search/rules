---
api_specs:
- filename: sportsgameodds-openapi.yml
  format: yaml
  label: SportsGameOdds API
  slug: sportsgameodds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsgameodds/refs/heads/main/openapi/sportsgameodds-openapi.yml
categories:
- sportsgameodds
description: Spectral linting rules defining API design standards and conventions for SportsGameOdds.
layout: rules
name: SportsGameOdds API Rules
provider_name: SportsGameOdds
provider_slug: sportsgameodds
rule_count: 9
rules:
- description: All operations must have exactly one tag from the approved list.
  given: $.paths[*][*]
  name: sportsgameodds-operation-tags
  severity: error
- description: Paths should end with a trailing slash per SportsGameOdds convention.
  given: $.paths
  name: sportsgameodds-paths-trailing-slash
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: sportsgameodds-operation-ids-camel-case
  severity: error
- description: All GET operations must define a 200 response.
  given: $.paths[*].get
  name: sportsgameodds-response-200-required
  severity: error
- description: All operations must use apiKeyHeader security scheme.
  given: $.paths[*][*]
  name: sportsgameodds-apikey-security
  severity: error
- description: Query parameter names must use camelCase.
  given: $.paths[*][*].parameters[?(@.in == 'query')].name
  name: sportsgameodds-query-param-names-camel-case
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sportsgameodds-summary-title-case
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: sportsgameodds-schemas-have-descriptions
  severity: warn
- description: Path parameters defined in operation must appear in the path.
  given: $.paths[*][*].parameters[?(@.in == 'path')].name
  name: sportsgameodds-path-params-in-path
  severity: error
rules_file: rules/sportsgameodds-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sportsgameodds/refs/heads/main/rules/sportsgameodds-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: sportsgameodds-rules
source_filename: sportsgameodds-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SportsGameOdds API-specific conventions\n\n  sportsgameodds-operation-tags:\n    description: All operations must have exactly one tag from the approved list.\n    message: \"Operation '{{property}}' must include a valid tag (Events, Teams, Players, Sports, Leagues, Stats, Markets, Account).\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n          maxItems: 1\n          items:\n            type: string\n            enum:\n              - Events\n              - Teams\n              - Players\n              - Sports\n              - Leagues\n              - Stats\n              - Markets\n              - Account\n\n  sportsgameodds-paths-trailing-slash:\n    description: Paths should end with a trailing slash per SportsGameOdds convention.\n    message: \"Path '{{property}}' should end with a trailing\
  \ slash (/).\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\/$\"\n\n  sportsgameodds-operation-ids-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sportsgameodds-response-200-required:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  sportsgameodds-apikey-security:\n    description: All operations must use apiKeyHeader security scheme.\n    message: \"Operation must require apiKeyHeader authentication.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n    \
  \  field: security\n      function: truthy\n\n  sportsgameodds-query-param-names-camel-case:\n    description: Query parameter names must use camelCase.\n    message: \"Query parameter '{{value}}' must use camelCase naming.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sportsgameodds-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  sportsgameodds-schemas-have-descriptions:\n    description: Schema properties should have descriptions.\n    message: \"Schema property should have a description.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n\
  \      field: description\n      function: truthy\n\n  sportsgameodds-path-params-in-path:\n    description: Path parameters defined in operation must appear in the path.\n    message: \"Path parameter '{{value}}' must be referenced in the path.\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sportsgameodds/refs/heads/main/rules/sportsgameodds-rules.yml
tags:
- Sports Betting
- Odds
- Sports Data
- Fantasy Sports
- Gambling
- Spectral
- Linting
- API Governance
---
