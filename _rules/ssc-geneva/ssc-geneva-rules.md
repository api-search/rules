---
api_specs:
- filename: ssc-geneva-fund-accounting-openapi.yml
  format: yaml
  label: SS&C Geneva Fund Accounting API
  slug: ssc-geneva-fund-accounting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ssc-geneva/refs/heads/main/openapi/ssc-geneva-fund-accounting-openapi.yml
categories:
- ssc
description: Spectral linting rules defining API design standards and conventions for SS&C Geneva.
layout: rules
name: SS&C Geneva API Rules
provider_name: SS&C Geneva
provider_slug: ssc-geneva
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ssc-geneva-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: ssc-geneva-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: ssc-geneva-tags-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][*].description
  name: ssc-geneva-description-required
  severity: warn
- description: Portfolio paths must include portfolioId as a path parameter
  given: $.paths[~/portfolios/{portfolioId}*]
  name: ssc-geneva-portfolio-id-path-param
  severity: warn
- description: Date query parameters should use ISO 8601 date format
  given: $.paths[*][*].parameters[?(@.in == 'query' && @.name =~ /[Dd]ate$/)]
  name: ssc-geneva-date-format-query-params
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: ssc-geneva-response-200-required
  severity: error
- description: Financial status and type enumerations should use SCREAMING_SNAKE_CASE
  given: $.components.schemas[*].properties[?(@.enum)]
  name: ssc-geneva-financial-enum-uppercase
  severity: hint
rules_file: rules/ssc-geneva-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ssc-geneva/refs/heads/main/rules/ssc-geneva-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 5
slug: ssc-geneva-rules
source_filename: ssc-geneva-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ssc-geneva-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s?)+$\"\n\n  ssc-geneva-operationid-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ssc-geneva-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  ssc-geneva-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  ssc-geneva-portfolio-id-path-param:\n    description:\
  \ Portfolio paths must include portfolioId as a path parameter\n    severity: warn\n    given: \"$.paths[~/portfolios/{portfolioId}*]\"\n    then:\n      function: truthy\n\n  ssc-geneva-date-format-query-params:\n    description: Date query parameters should use ISO 8601 date format\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'query' && @.name =~ /[Dd]ate$/)]\"\n    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n          - date-time\n\n  ssc-geneva-response-200-required:\n    description: All GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  ssc-geneva-financial-enum-uppercase:\n    description: Financial status and type enumerations should use SCREAMING_SNAKE_CASE\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@.enum)]\"\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          type: object\n          properties:\n            enum:\n              type: array\n              items:\n                type: string\n                pattern: \"^[A-Z_]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ssc-geneva/refs/heads/main/rules/ssc-geneva-rules.yml
tags:
- Fund Accounting
- Asset Management
- Portfolio Management
- Financial Services
- Hedge Funds
- NAV Calculation
- Spectral
- Linting
- API Governance
---
