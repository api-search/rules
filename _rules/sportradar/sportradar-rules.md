---
api_specs:
- filename: sportradar-sports-data-openapi.yml
  format: yaml
  label: Sportradar Sports Data API
  slug: sports-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sportradar/refs/heads/main/openapi/sportradar-sports-data-openapi.yml
categories:
- sportradar
description: Spectral linting rules defining API design standards and conventions for Sportradar.
layout: rules
name: Sportradar API Rules
provider_name: Sportradar
provider_slug: sportradar
rule_count: 12
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: sportradar-operation-id-required
  severity: error
- description: operationId must start with a standard REST verb (get, list, create, update, delete).
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sportradar-operation-id-verb-prefix
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sportradar-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: sportradar-tags-required
  severity: warn
- description: API must define apiKey security scheme.
  given: $.components.securitySchemes
  name: sportradar-api-key-auth-required
  severity: error
- description: Every operation must define a 200 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sportradar-response-200-required
  severity: error
- description: Every operation must define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sportradar-401-response-required
  severity: warn
- description: Every operation should define a 429 Too Many Requests response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sportradar-429-rate-limit-response
  severity: info
- description: Paths should include sport or competition prefix (e.g., /nba/, /nfl/, /soccer/).
  given: $.paths
  name: sportradar-path-sport-prefix
  severity: info
- description: Sportradar endpoints use .json suffix for JSON responses.
  given: $.paths
  name: sportradar-json-response-suffix
  severity: info
- description: The API must define at least one server.
  given: $
  name: sportradar-servers-required
  severity: error
- description: The info object must include a contact entry.
  given: $.info
  name: sportradar-info-contact-required
  severity: warn
rules_file: rules/sportradar-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sportradar/refs/heads/main/rules/sportradar-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 3
  warn: 5
slug: sportradar-rules
source_filename: sportradar-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  sportradar-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sportradar-operation-id-verb-prefix:\n    description: operationId must start with a standard REST verb (get, list, create, update, delete).\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(get|list|create|update|delete)[A-Z][a-zA-Z0-9]+$\"\n\n  sportradar-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /-]+$\"\n\n  sportradar-tags-required:\n    description: Every\
  \ operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  sportradar-api-key-auth-required:\n    description: API must define apiKey security scheme.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: apiKey\n      function: truthy\n\n  sportradar-response-200-required:\n    description: Every operation must define a 200 success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n\n  sportradar-401-response-required:\n    description: Every operation must define a 401 Unauthorized response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  sportradar-429-rate-limit-response:\n\
  \    description: Every operation should define a 429 Too Many Requests response.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"429\"]\n\n  sportradar-path-sport-prefix:\n    description: Paths should include sport or competition prefix (e.g., /nba/, /nfl/, /soccer/).\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(nba|nfl|nhl|mlb|soccer|tennis|golf|esports|mma|cricket|rugby)\"\n\n  sportradar-json-response-suffix:\n    description: Sportradar endpoints use .json suffix for JSON responses.\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\.json$\"\n\n  sportradar-servers-required:\n    description: The API must define at least one server.\n    severity: error\n    given: \"$\"\n    then:\n      field:\
  \ servers\n      function: truthy\n\n  sportradar-info-contact-required:\n    description: The info object must include a contact entry.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sportradar/refs/heads/main/rules/sportradar-rules.yml
tags:
- Data
- Esports
- Fantasy Sports
- Media
- Real-Time
- Sports
- Sports Data
- Statistics
- Spectral
- Linting
- API Governance
---
