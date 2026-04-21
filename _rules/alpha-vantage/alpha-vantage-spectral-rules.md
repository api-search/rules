---
categories:
- alpha
description: Spectral linting rules defining API design standards and conventions for Alpha Vantage.
layout: rules
name: Alpha Vantage API Rules
provider_name: Alpha Vantage
provider_slug: alpha-vantage
rule_count: 15
rules:
- description: All operation summaries must start with "Alpha Vantage"
  given: $.paths[*][*].summary
  name: alpha-vantage-operation-summary-prefix
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: alpha-vantage-operation-tags
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: alpha-vantage-operation-id
  severity: error
- description: All operations must have a description
  given: $.paths[*][*]
  name: alpha-vantage-operation-description
  severity: warn
- description: All operations must have the apikey parameter
  given: $.paths[*][get].parameters[*]
  name: alpha-vantage-apikey-param
  severity: error
- description: All query operations must have the function parameter
  given: $.paths[/query][get].parameters[?(@.name == 'function')]
  name: alpha-vantage-function-param
  severity: error
- description: The function parameter must have an enum of allowed values
  given: $.paths[/query][get].parameters[?(@.name == 'function')].schema
  name: alpha-vantage-function-enum
  severity: warn
- description: API must define the ApiKey security scheme
  given: $.components.securitySchemes
  name: alpha-vantage-apikey-security-scheme
  severity: error
- description: ApiKey must be passed as a query parameter
  given: $.components.securitySchemes.ApiKey
  name: alpha-vantage-apikey-in-query
  severity: error
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: alpha-vantage-schema-title
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: alpha-vantage-schema-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: alpha-vantage-property-description
  severity: warn
- description: All operations must document a 200 success response
  given: $.paths[*][*].responses
  name: alpha-vantage-200-response
  severity: error
- description: All operations should have x-microcks-operation extension
  given: $.paths[*][*]
  name: alpha-vantage-microcks-operation
  severity: info
- description: API server must use HTTPS
  given: $.servers[*].url
  name: alpha-vantage-server-https
  severity: error
rules_file: rules/alpha-vantage-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/alpha-vantage/refs/heads/main/rules/alpha-vantage-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 1
  warn: 6
slug: alpha-vantage-spectral-rules
tags:
- Financial
- Market Data
- Stocks
- Technical Indicators
- Economic Data
- Sentiment Analysis
- Spectral
- Linting
- API Governance
---
