---
categories:
- binance
description: Spectral linting rules defining API design standards and conventions for Binance.
layout: rules
name: Binance API Rules
provider_name: Binance
provider_slug: binance
rule_count: 24
rules:
- description: API title must start with "Binance"
  given: $.info.title
  name: binance-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: binance-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: binance-info-contact-present
  severity: warn
- description: Operation summaries must start with "Binance"
  given: $.paths[*][*].summary
  name: binance-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: binance-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: binance-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: binance-operation-description-present
  severity: warn
- description: Path segments must use kebab-case or standard patterns
  given: $.paths
  name: binance-path-kebab-case
  severity: warn
- description: POST operations must have a request body
  given: $.paths[*].post
  name: binance-request-body-post
  severity: error
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: binance-response-success-present
  severity: error
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: binance-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: binance-schema-description-present
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: binance-security-scheme-present
  severity: error
- description: Binance APIs use HMAC SHA256 signed requests
  given: $.components.securitySchemes[*]
  name: binance-hmac-auth-used
  severity: warn
- description: Private operations must declare security
  given: $.paths[*][post,delete]
  name: binance-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: binance-tags-defined
  severity: warn
- description: API must define servers
  given: $
  name: binance-servers-present
  severity: error
- description: Server URL must use HTTPS
  given: $.servers[*].url
  name: binance-server-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: binance-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: binance-microcks-operation-present
  severity: warn
- description: Signed endpoints should include timestamp parameter
  given: $.paths[*][get,post,delete].parameters[?(@.name=='timestamp')]
  name: binance-timestamp-parameter
  severity: warn
- description: Signed endpoints may include recvWindow parameter
  given: $.paths[*][*].parameters[?(@.name=='recvWindow')]
  name: binance-recvwindow-parameter
  severity: info
- description: API info must include license
  given: $.info
  name: binance-license-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: binance-schema-properties-described
  severity: warn
rules_file: rules/binance-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/rules/binance-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 1
  warn: 15
slug: binance-spectral-rules
tags:
- Cryptocurrency
- Exchange
- Trading
- Blockchain
- Finance
- DeFi
- Market Data
- Spectral
- Linting
- API Governance
---
