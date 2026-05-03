---
api_specs:
- filename: wager-api-openapi.yml
  format: yaml
  label: Wager API - Sports Odds
  slug: wager-api-odds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wager-api/refs/heads/main/openapi/wager-api-openapi.yml
- filename: wager-api-openapi.yml
  format: yaml
  label: Wager API - Fantasy Sports Data
  slug: wager-api-fantasy
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wager-api/refs/heads/main/openapi/wager-api-openapi.yml
categories:
- wager
description: Spectral linting rules defining API design standards and conventions for Wager API.
layout: rules
name: Wager API API Rules
provider_name: Wager API
provider_slug: wager-api
rule_count: 8
rules:
- description: Wager API requires X-API-Key header authentication
  given: $.components.securitySchemes
  name: wager-api-key-header
  severity: error
- description: All Wager API paths must be versioned with /v1/ prefix
  given: $.paths
  name: wager-api-versioned-paths
  severity: error
- description: Odds and data endpoints should document the sport parameter
  given: $.paths[/v1/odds,/v1/props,/v1/futures,/v1/injuries,/v1/depth-charts][get].parameters
  name: wager-api-sport-parameter
  severity: warn
- description: All Wager API operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: wager-api-operation-ids
  severity: error
- description: All Wager API operation summaries should use Title Case
  given: $.paths[*][get,post,put,patch,delete]
  name: wager-api-summaries-title-case
  severity: warn
- description: Wager API list endpoints should use data envelope in responses
  given: $.paths[*][get].responses[200].content.application/json.schema.properties
  name: wager-api-response-envelope
  severity: warn
- description: Wager API servers must use HTTPS
  given: $.servers[*].url
  name: wager-api-https-only
  severity: error
- description: Path segments should use kebab-case
  given: $.paths
  name: wager-api-path-params-kebab
  severity: warn
rules_file: rules/wager-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wager-api/refs/heads/main/rules/wager-api-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: wager-api-rules
source_filename: wager-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\nrules:\n  wager-api-key-header:\n    description: Wager API requires X-API-Key header authentication\n    message: \"Wager API must use X-API-Key header for authentication\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"apiKey\"\n\n  wager-api-versioned-paths:\n    description: All Wager API paths must be versioned with /v1/ prefix\n    message: \"API paths must include /v1/ version prefix\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^/v[0-9]+/\":\n              type: object\n\n  wager-api-sport-parameter:\n    description: Odds and data endpoints should document the sport parameter\n    message: \"Sports data endpoints should include\
  \ sport parameter\"\n    severity: warn\n    given: \"$.paths[/v1/odds,/v1/props,/v1/futures,/v1/injuries,/v1/depth-charts][get].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: sport\n\n  wager-api-operation-ids:\n    description: All Wager API operations must have operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wager-api-summaries-title-case:\n    description: All Wager API operation summaries should use Title Case\n    message: \"Operation summary should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  wager-api-response-envelope:\n    description:\
  \ Wager API list endpoints should use data envelope in responses\n    message: \"List responses should wrap results in a data array\"\n    severity: warn\n    given: \"$.paths[*][get].responses[200].content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"data\"]\n            - required: [\"results\"]\n\n  wager-api-https-only:\n    description: Wager API servers must use HTTPS\n    message: \"Server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  wager-api-path-params-kebab:\n    description: Path segments should use kebab-case\n    message: \"Path segments should be kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9]+/[a-z][a-z0-9-]*(/\\\\{[a-zA-Z]+\\\
  \\})?((/[a-z][a-z0-9-]*)*(/\\\\{[a-zA-Z]+\\\\})*)*)$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wager-api/refs/heads/main/rules/wager-api-rules.yml
tags:
- Sports Betting
- Sports Odds
- Fantasy Sports
- Sports Data
- NFL
- NBA
- MLB
- NHL
- NCAA
- Spectral
- Linting
- API Governance
---
