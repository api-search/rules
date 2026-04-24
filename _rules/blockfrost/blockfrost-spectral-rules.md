---
categories:
- external
- get
- info
- 'no'
- openapi
- operation
- pagination
- parameter
- paths
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Blockfrost.
layout: rules
name: Blockfrost API Rules
provider_name: Blockfrost
provider_slug: blockfrost
rule_count: 30
rules:
- description: API title must start with "Blockfrost"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: Info object must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Info object must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info object should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Info object should have license information
  given: $.info
  name: info-license-required
  severity: info
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Path segments must use lowercase with underscores or kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Blockfrost"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use snake_case
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-snake-case
  severity: info
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must define a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: List endpoints should support count pagination parameter
  given: $.paths[*].get
  name: pagination-count-or-limit
  severity: info
- description: Every operation must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: Operations should define a 400 Bad Request response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-400-defined
  severity: info
- description: Operations should define a 403 Forbidden response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-403-defined
  severity: info
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas must have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: At least one security scheme must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security must be defined
  given: $
  name: security-global-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Global tags array should be defined
  given: $
  name: tags-global-defined
  severity: info
- description: External documentation should be provided
  given: $
  name: external-docs-encouraged
  severity: info
rules_file: rules/blockfrost-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/blockfrost/refs/heads/main/rules/blockfrost-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 7
  warn: 10
slug: blockfrost-spectral-rules
tags:
- Blockchain
- Cardano
- Cryptocurrency
- DApps
- NFT
- Web3
- Spectral
- Linting
- API Governance
---
