---
api_specs:
- filename: sportsdataio-nfl-openapi.yml
  format: yaml
  label: SportsDataIO NFL API
  slug: sportsdataio-nfl
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/openapi/sportsdataio-nfl-openapi.yml
- filename: sportsdataio-mlb-openapi.yml
  format: yaml
  label: SportsDataIO MLB API
  slug: sportsdataio-mlb
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/openapi/sportsdataio-mlb-openapi.yml
- filename: sportsdataio-nba-openapi.yml
  format: yaml
  label: SportsDataIO NBA API
  slug: sportsdataio-nba
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/openapi/sportsdataio-nba-openapi.yml
- filename: sportsdataio-nhl-openapi.yml
  format: yaml
  label: SportsDataIO NHL API
  slug: sportsdataio-nhl
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/openapi/sportsdataio-nhl-openapi.yml
- filename: sportsdataio-soccer-openapi.yml
  format: yaml
  label: SportsDataIO Soccer API
  slug: sportsdataio-soccer
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/openapi/sportsdataio-soccer-openapi.yml
categories:
- sportsdataio
description: Spectral linting rules defining API design standards and conventions for SportsDataIO.
layout: rules
name: SportsDataIO API Rules
provider_name: SportsDataIO
provider_slug: sportsdataio
rule_count: 9
rules:
- description: SportsDataIO endpoints use a {format} path parameter for JSON or XML.
  given: $.paths
  name: sportsdataio-format-param
  severity: warn
- description: SportsDataIO endpoints use a /v3/{sport}/ prefix.
  given: $.paths
  name: sportsdataio-v3-prefix
  severity: error
- description: All operations must use API key authentication.
  given: $.paths[*][*]
  name: sportsdataio-apikey-security
  severity: error
- description: SportsDataIO APIs are read-only and use only GET requests.
  given: $.paths[*]
  name: sportsdataio-get-only
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: sportsdataio-operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sportsdataio-summary-title-case
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths[*].get
  name: sportsdataio-response-200
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: sportsdataio-operation-id
  severity: error
- description: API must define production server URL.
  given: $.servers[*].url
  name: sportsdataio-server-production
  severity: error
rules_file: rules/sportsdataio-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/rules/sportsdataio-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 3
slug: sportsdataio-rules
source_filename: sportsdataio-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SportsDataIO API-specific conventions\n\n  sportsdataio-format-param:\n    description: SportsDataIO endpoints use a {format} path parameter for JSON or XML.\n    message: \"Path '{{property}}' should include a {format} parameter for content-type negotiation.\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{format\\\\}.*\"\n\n  sportsdataio-v3-prefix:\n    description: SportsDataIO endpoints use a /v3/{sport}/ prefix.\n    message: \"Path '{{property}}' must include /v3/ version prefix.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v3\\\\/\"\n\n  sportsdataio-apikey-security:\n    description: All operations must use API key authentication.\n    message: \"Operation must use apiKeyHeader or apiKeyQuery authentication.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n   \
  \ then:\n      field: security\n      function: truthy\n\n  sportsdataio-get-only:\n    description: SportsDataIO APIs are read-only and use only GET requests.\n    message: \"Only GET operations are expected in SportsDataIO APIs.\"\n    severity: warn\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          not:\n            required:\n              - post\n\n  sportsdataio-operation-summary:\n    description: All operations must have a summary.\n    message: \"Operation must have a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  sportsdataio-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\\
  s[A-Z][a-zA-Z]*)*$\"\n\n  sportsdataio-response-200:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  sportsdataio-operation-id:\n    description: All operations must have an operationId.\n    message: \"Operation must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sportsdataio-server-production:\n    description: API must define production server URL.\n    message: \"API must define https://api.sportsdata.io as the production server.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.sportsdata\\\\.io$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sportsdataio/refs/heads/main/rules/sportsdataio-rules.yml
tags:
- Sports Data
- Statistics
- Live Scores
- Fantasy Sports
- Odds
- NFL
- NBA
- MLB
- NHL
- Soccer
- Spectral
- Linting
- API Governance
---
