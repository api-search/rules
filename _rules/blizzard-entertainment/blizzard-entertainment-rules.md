---
api_specs:
- filename: blizzard-world-of-warcraft-openapi.yml
  format: yaml
  label: World of Warcraft Game Data API
  slug: world-of-warcraft-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/openapi/blizzard-world-of-warcraft-openapi.yml
- filename: blizzard-diablo-iii-openapi.yml
  format: yaml
  label: Diablo III Community API
  slug: diablo-iii-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/openapi/blizzard-diablo-iii-openapi.yml
- filename: blizzard-starcraft-ii-openapi.yml
  format: yaml
  label: StarCraft II Community API
  slug: starcraft-ii-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/openapi/blizzard-starcraft-ii-openapi.yml
- filename: blizzard-hearthstone-openapi.yml
  format: yaml
  label: Hearthstone Game Data API
  slug: hearthstone-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/openapi/blizzard-hearthstone-openapi.yml
- filename: blizzard-oauth-openapi.yml
  format: yaml
  label: Battle.net OAuth API
  slug: oauth-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/openapi/blizzard-oauth-openapi.yml
categories:
- blizzard
description: Spectral linting rules defining API design standards and conventions for Blizzard Entertainment.
layout: rules
name: Blizzard Entertainment API Rules
provider_name: Blizzard Entertainment
provider_slug: blizzard-entertainment
rule_count: 5
rules:
- description: Battle.net APIs must declare a Battle.net Developer Portal contact.
  given: $.info
  name: blizzard-info-contact-defined
  severity: error
- description: Servers must use a Battle.net regional host (us, eu, kr, tw, cn) or oauth.battle.net.
  given: $.servers[*].url
  name: blizzard-server-regional-host
  severity: error
- description: Game Data and Profile endpoints require bearer-token auth.
  given: $.components.securitySchemes.bearerAuth
  name: blizzard-bearer-auth-required
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: blizzard-operation-summary-title-case
  severity: warn
- description: Game Data endpoints should accept a namespace query parameter.
  given: $.paths['/data/wow/realm/index'].get
  name: blizzard-namespace-parameter
  severity: warn
rules_file: rules/blizzard-entertainment-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/rules/blizzard-entertainment-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 3
slug: blizzard-entertainment-rules
source_filename: blizzard-entertainment-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nformats:\n  - oas3\nrules:\n  blizzard-info-contact-defined:\n    description: Battle.net APIs must declare a Battle.net Developer Portal contact.\n    message: \"{{description}}\"\n    given: $.info\n    severity: error\n    then:\n      field: contact\n      function: truthy\n\n  blizzard-server-regional-host:\n    description: Servers must use a Battle.net regional host (us, eu, kr, tw, cn) or oauth.battle.net.\n    message: \"Server URL '{{value}}' should be a battle.net or blizzard.com host\"\n    given: $.servers[*].url\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://([a-z]{2}\\\\.api\\\\.blizzard\\\\.com|oauth\\\\.battle\\\\.net)\"\n\n  blizzard-bearer-auth-required:\n    description: Game Data and Profile endpoints require bearer-token auth.\n    message: \"Security scheme must use OAuth 2.0 bearer tokens\"\n    given: $.components.securitySchemes.bearerAuth\n    severity: warn\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - type\n            - scheme\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  blizzard-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' should be in Title Case\"\n    given: $.paths.*.*.summary\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s+[A-Z][a-zA-Z0-9]*)*$\"\n\n  blizzard-namespace-parameter:\n    description: Game Data endpoints should accept a namespace query parameter.\n    message: \"Game Data endpoint should declare the namespace parameter\"\n    given: \"$.paths['/data/wow/realm/index'].get\"\n    severity: warn\n    then:\n      field: parameters\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/blizzard-entertainment/refs/heads/main/rules/blizzard-entertainment-rules.yml
tags:
- Games
- Entertainment
- Video Games
- Game Data
- Battle.net
- Spectral
- Linting
- API Governance
---
