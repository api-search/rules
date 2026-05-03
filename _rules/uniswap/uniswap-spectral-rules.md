---
api_specs:
- filename: uniswap-trading-openapi.yaml
  format: yaml
  label: Uniswap Trading API
  slug: uniswap-trading-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniswap/refs/heads/main/openapi/uniswap-trading-openapi.yaml
categories:
- components
- delete
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- post
- request
- response
- schema
- security
- server
- servers
description: Spectral linting rules defining API design standards and conventions for Uniswap.
layout: rules
name: Uniswap API Rules
provider_name: Uniswap
provider_slug: uniswap
rule_count: 33
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.info
  name: info-description-required
  severity: warn
- description: ''
  given: $.info
  name: info-version-required
  severity: error
- description: ''
  given: $
  name: openapi-version-3
  severity: error
- description: ''
  given: $
  name: servers-defined
  severity: error
- description: ''
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: ''
  given: $.servers[*]
  name: server-description-required
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-no-query-strings
  severity: error
- description: ''
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-id-snake-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: ''
  given: $.paths[*][post,get]
  name: response-401-unauthorized
  severity: warn
- description: ''
  given: $.paths[*][post,get]
  name: response-429-rate-limit
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camel-case
  severity: info
- description: ''
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: error
- description: ''
  given: $.components.securitySchemes[*][?(@.type=='apiKey')]
  name: security-api-key-header
  severity: error
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: ''
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: ''
  given: $.paths[*].post
  name: post-should-have-request-body
  severity: info
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.components
  name: components-schemas-defined
  severity: info
rules_file: rules/uniswap-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uniswap/refs/heads/main/rules/uniswap-spectral-rules.yml
severity_counts:
  error: 14
  hint: 0
  info: 4
  warn: 15
slug: uniswap-spectral-rules
source_filename: uniswap-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # ─── INFO / METADATA ───────────────────────────────────────────────────────\n\n  info-title-required:\n    message: API info title is required\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    message: API info description is required and should be meaningful\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: API info version is required\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # ─── OPENAPI VERSION ────────────────────────────────────────────────────────\n\n  openapi-version-3:\n    message: OpenAPI version must be 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # ─── SERVERS ────────────────────────────────────────────────────────────────\n\
  \n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  server-description-required:\n    message: Server entries should have descriptions\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # ─── PATHS — NAMING CONVENTIONS ─────────────────────────────────────────────\n\n  paths-no-trailing-slash:\n    message: Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-no-query-strings:\n    message: Query strings must not appear in path definitions\n    severity: error\n    given: $.paths[*]~\n\
  \    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  paths-kebab-case:\n    message: Path segments should use kebab-case (lowercase with hyphens)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9_{}/-]+)+$\"\n\n  # ─── OPERATIONS ─────────────────────────────────────────────────────────────\n\n  operation-id-required:\n    message: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-snake-case:\n    message: operationId should use snake_case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  operation-summary-required:\n    message: Every operation must have a summary\n\
  \    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    message: Operation summaries should use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-description-required:\n    message: Every operation should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    message: Every operation should have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # ─── PARAMETERS ─────────────────────────────────────────────────────────────\n\n  parameter-description-required:\n    message:\
  \ All parameters must have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    message: All parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # ─── REQUEST BODIES ──────────────────────────────────────────────────────────\n\n  request-body-description:\n    message: Request bodies should have a description\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  request-body-json-content:\n    message: Request bodies should define application/json content\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n        \
  \  type: object\n          minProperties: 1\n\n  # ─── RESPONSES ───────────────────────────────────────────────────────────────\n\n  response-success-required:\n    message: Every operation must define at least one 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2[0-9]{2}$\": {}\n          minProperties: 1\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-unauthorized:\n    message: Authenticated APIs should define a 401 response\n    severity: warn\n    given: $.paths[*][post,get]\n    then:\n      field: responses.401\n      function: truthy\n\n  response-429-rate-limit:\n  \
  \  message: APIs with rate limits should define a 429 response\n    severity: info\n    given: $.paths[*][post,get]\n    then:\n      field: responses.429\n      function: truthy\n\n  # ─── SCHEMAS — PROPERTY NAMING ───────────────────────────────────────────────\n\n  schema-property-camel-case:\n    message: Schema properties should use camelCase (Uniswap convention)\n    severity: info\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-type-defined:\n    message: Schema objects should define a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # ─── SECURITY ────────────────────────────────────────────────────────────────\n\n  security-schemes-defined:\n    message: Security schemes must be defined\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\
  \n  security-api-key-header:\n    message: API key should be passed in x-api-key header (not as a query param)\n    severity: error\n    given: $.components.securitySchemes[*][?(@.type=='apiKey')]\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values:\n          - header\n\n  # ─── HTTP METHOD CONVENTIONS ─────────────────────────────────────────────────\n\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    message: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  post-should-have-request-body:\n    message: POST operations should typically include a request body\n    severity: info\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function:\
  \ truthy\n\n  # ─── GENERAL QUALITY ─────────────────────────────────────────────────────────\n\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  components-schemas-defined:\n    message: Components schemas section should be defined for reusable types\n    severity: info\n    given: $.components\n    then:\n      field: schemas\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uniswap/refs/heads/main/rules/uniswap-spectral-rules.yml
tags:
- Blockchain
- Cryptocurrency
- DeFi
- Decentralized Exchange
- Liquidity
- Swaps
- Spectral
- Linting
- API Governance
---
