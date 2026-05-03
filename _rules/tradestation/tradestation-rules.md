---
api_specs:
- filename: tradestation-api-openapi.yml
  format: yaml
  label: TradeStation API
  slug: tradestation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/openapi/tradestation-api-openapi.yml
- filename: tradestation-streaming-asyncapi.yml
  format: yaml
  label: TradeStation Streaming API
  slug: tradestation-streaming
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/asyncapi/tradestation-streaming-asyncapi.yml
categories:
- tradestation
description: Spectral linting rules defining API design standards and conventions for TradeStation.
layout: rules
name: TradeStation API Rules
provider_name: TradeStation
provider_slug: tradestation
rule_count: 11
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: tradestation-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: tradestation-operation-ids-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][*]
  name: tradestation-operation-description-required
  severity: warn
- description: API must use OAuth2 authorization code authentication.
  given: $.components.securitySchemes.oauth2AuthCode
  name: tradestation-oauth2-required
  severity: error
- description: All API paths must use the /v3/ version prefix.
  given: $.paths[*]~
  name: tradestation-versioned-paths
  severity: error
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: tradestation-tags-required
  severity: warn
- description: Schema property names must use PascalCase to match TradeStation API conventions.
  given: $.components.schemas[*].properties[*]~
  name: tradestation-pascal-case-schema-properties
  severity: warn
- description: All operations must define a 200 success response.
  given: $.paths[*][*].responses
  name: tradestation-response-200-defined
  severity: error
- description: All operations must define a 401 unauthorized response.
  given: $.paths[*][*].responses
  name: tradestation-response-401-defined
  severity: warn
- description: POST operations must define a requestBody.
  given: $.paths[*][post]
  name: tradestation-post-request-body
  severity: error
- description: OrderRequest must define AccountID, Symbol, Quantity, OrderType, TradeAction, TimeInForce as required.
  given: $.components.schemas.OrderRequest.required
  name: tradestation-order-required-fields
  severity: error
rules_file: rules/tradestation-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/rules/tradestation-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 5
slug: tradestation-rules
source_filename: tradestation-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tradestation-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  tradestation-operation-ids-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: defined\n\n  tradestation-operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: defined\n\n  tradestation-oauth2-required:\n    description: API must use OAuth2 authorization code authentication.\n    severity: error\n    given: \"$.components.securitySchemes.oauth2AuthCode\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          properties:\n            type:\n              const: oauth2\n\n  tradestation-versioned-paths:\n    description: All API paths must use the /v3/ version prefix.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v3/\"\n\n  tradestation-tags-required:\n    description: All operations must be tagged.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  tradestation-pascal-case-schema-properties:\n    description: Schema property names must use PascalCase to match TradeStation API conventions.\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  tradestation-response-200-defined:\n    description: All operations must define a 200 success response.\n    severity: error\n    given:\
  \ \"$.paths[*][*].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  tradestation-response-401-defined:\n    description: All operations must define a 401 unauthorized response.\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  tradestation-post-request-body:\n    description: POST operations must define a requestBody.\n    severity: error\n    given: \"$.paths[*][post]\"\n    then:\n      field: requestBody\n      function: defined\n\n  tradestation-order-required-fields:\n    description: OrderRequest must define AccountID, Symbol, Quantity, OrderType, TradeAction, TimeInForce as required.\n    severity: error\n    given: \"$.components.schemas.OrderRequest.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: AccountID\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/rules/tradestation-rules.yml
tags:
- Brokerage
- Cryptocurrency
- Finance
- Futures
- Market Data
- Options
- Stocks
- Trading
- Spectral
- Linting
- API Governance
---
