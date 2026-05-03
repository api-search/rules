---
api_specs:
- filename: stockdata-openapi.yml
  format: yaml
  label: StockData API
  slug: stockdata
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stockdata/refs/heads/main/openapi/stockdata-openapi.yml
categories:
- stockdata
description: Spectral linting rules defining API design standards and conventions for StockData.
layout: rules
name: StockData API Rules
provider_name: StockData
provider_slug: stockdata
rule_count: 8
rules:
- description: All StockData API endpoints must require the api_token query parameter.
  given: $.paths.*.*.parameters[?(@.name == 'api_token')]
  name: stockdata-api-token-required
  severity: error
- description: StockData operationIds must use camelCase to match the existing SDK conventions.
  given: $.paths[*][*].operationId
  name: stockdata-operationid-camel-case
  severity: warn
- description: All tags on operations must use Title Case.
  given: $.paths[*][*].tags[*]
  name: stockdata-tags-title-case
  severity: warn
- description: All StockData GET operations must define a 200 success response.
  given: $.paths[*].get
  name: stockdata-response-200-required
  severity: error
- description: Collection endpoints returning lists should support page and limit query parameters for pagination.
  given: $.paths[*].get[?(@.operationId =~ /^(get|list|search)/)]
  name: stockdata-pagination-params
  severity: info
- description: All parameters must have non-empty descriptions.
  given: $.paths[*][*].parameters[*]
  name: stockdata-no-empty-descriptions
  severity: warn
- description: The symbols parameter must clearly state it accepts comma-separated ticker symbols.
  given: $.paths[*][*].parameters[?(@.name == 'symbols')]
  name: stockdata-symbols-param-description
  severity: info
- description: The StockData API server URL must include /v1 in the base path.
  given: $.servers[*].url
  name: stockdata-server-v1-prefix
  severity: error
rules_file: rules/stockdata-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stockdata/refs/heads/main/rules/stockdata-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 3
slug: stockdata-rules
source_filename: stockdata-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stockdata-api-token-required:\n    description: All StockData API endpoints must require the api_token query parameter.\n    message: \"Missing required api_token query parameter on operation '{{operationId}}'.\"\n    severity: error\n    given: \"$.paths.*.*.parameters[?(@.name == 'api_token')]\"\n    then:\n      field: required\n      function: truthy\n\n  stockdata-operationid-camel-case:\n    description: >-\n      StockData operationIds must use camelCase to match the existing SDK\n      conventions.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stockdata-tags-title-case:\n    description: All tags on operations must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  stockdata-response-200-required:\n    description: All StockData GET operations must define a 200 success response.\n    message: \"Operation '{{operationId}}' is missing a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  stockdata-pagination-params:\n    description: >-\n      Collection endpoints returning lists should support page and limit\n      query parameters for pagination.\n    message: \"List operation '{{operationId}}' should define 'page' and 'limit' parameters.\"\n    severity: info\n    given: \"$.paths[*].get[?(@.operationId =~ /^(get|list|search)/)]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n\n  stockdata-no-empty-descriptions:\n    description: All parameters must have non-empty\
  \ descriptions.\n    message: \"Parameter '{{path}}' must have a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  stockdata-symbols-param-description:\n    description: >-\n      The symbols parameter must clearly state it accepts comma-separated\n      ticker symbols.\n    message: \"The 'symbols' parameter description should mention comma-separated ticker symbols.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'symbols')]\"\n    then:\n      field: description\n      function: truthy\n\n  stockdata-server-v1-prefix:\n    description: The StockData API server URL must include /v1 in the base path.\n    message: \"StockData server URL must include /v1.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/v1$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stockdata/refs/heads/main/rules/stockdata-rules.yml
tags:
- Finance
- Financial Data
- Stock Market
- Market Data
- News
- Sentiment Analysis
- Spectral
- Linting
- API Governance
---
