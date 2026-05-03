---
api_specs:
- filename: union-pacific-api.yaml
  format: yaml
  label: Union Pacific API
  slug: union-pacific
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/union-pacific/refs/heads/main/openapi/union-pacific-api.yaml
categories:
- components
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- rpc
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Union Pacific.
layout: rules
name: Union Pacific API Rules
provider_name: Union Pacific
provider_slug: union-pacific
rule_count: 31
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.info.title
  name: info-title-contains-union-pacific
  severity: warn
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
  given: $.paths[*]~
  name: paths-camel-case-convention
  severity: info
- description: ''
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-id-camel-case
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
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: response-401-unauthorized
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch]
  name: response-400-bad-request
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camel-case
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: error
- description: ''
  given: $.components.securitySchemes[*]
  name: security-oauth2-present
  severity: warn
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: ''
  given: $.paths[?(@property =~ /release|order|cancel/)][*]
  name: rpc-style-post
  severity: info
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.components
  name: components-schemas-defined
  severity: error
rules_file: rules/union-pacific-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/union-pacific/refs/heads/main/rules/union-pacific-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 3
  warn: 15
slug: union-pacific-spectral-rules
source_filename: union-pacific-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # ─── INFO / METADATA ───────────────────────────────────────────────────────\n\n  info-title-required:\n    message: API info title is required\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-title-contains-union-pacific:\n    message: API title should reference Union Pacific\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)union.pacific\"\n\n  info-description-required:\n    message: API info description is required\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: API info version is required\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # ─── OPENAPI VERSION ────────────────────────────────────────────────────────\n\n  openapi-version-3:\n    message: OpenAPI version must be 3.x\n\
  \    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # ─── SERVERS ────────────────────────────────────────────────────────────────\n\n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # ─── PATHS — NAMING CONVENTIONS ─────────────────────────────────────────────\n\n  paths-camel-case-convention:\n    message: Paths use camelCase or lowercase for resource names (Union Pacific convention)\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9_{}/-]+)+$\"\n\n  paths-no-trailing-slash:\n    message:\
  \ Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # ─── OPERATIONS ─────────────────────────────────────────────────────────────\n\n  operation-id-required:\n    message: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    message: operationId should use camelCase (Union Pacific convention)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-summary-required:\n    message: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function:\
  \ truthy\n\n  operation-summary-title-case:\n    message: Operation summaries should use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-description-required:\n    message: Every operation should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    message: Every operation should have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # ─── PARAMETERS ─────────────────────────────────────────────────────────────\n\n  parameter-description-required:\n    message: All parameters should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n\
  \    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    message: All parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # ─── REQUEST BODIES ──────────────────────────────────────────────────────────\n\n  request-body-json:\n    message: Request bodies should use application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  request-body-description:\n    message: Request bodies should have a description\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  # ─── RESPONSES ───────────────────────────────────────────────────────────────\n\n  response-success-defined:\n\
  \    message: Every operation must define at least one 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: truthy\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-unauthorized:\n    message: Protected operations should define 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses.401\n      function: truthy\n\n  response-400-bad-request:\n    message: Write operations should define 400 Bad Request response\n    severity: info\n    given: $.paths[*][post,put,patch]\n    then:\n      field: responses.400\n      function: truthy\n\n  # ─── SCHEMAS — PROPERTY NAMING ───────────────────────────────────────────────\n\n  schema-property-camel-case:\n\
  \    message: Schema properties should use camelCase (Union Pacific convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-description-required:\n    message: Top-level component schemas should have descriptions\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # ─── SECURITY ────────────────────────────────────────────────────────────────\n\n  security-schemes-defined:\n    message: Security schemes must be defined\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-oauth2-present:\n    message: Union Pacific uses OAuth 2.0 Client Credentials authentication\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n \
  \       values:\n          - oauth2\n\n  # ─── HTTP METHOD CONVENTIONS ─────────────────────────────────────────────────\n\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  rpc-style-post:\n    message: >-\n      RPC-style action operations (releaseShipment, orderEquipment, cancelRequest)\n      should use POST method\n    severity: info\n    given: $.paths[?(@property =~ /release|order|cancel/)][*]\n    then:\n      function: truthy\n\n  # ─── GENERAL QUALITY ─────────────────────────────────────────────────────────\n\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  components-schemas-defined:\n    message: Components schemas section should be defined\n    severity: error\n    given:\
  \ $.components\n    then:\n      field: schemas\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/union-pacific/refs/heads/main/rules/union-pacific-spectral-rules.yml
tags:
- Freight
- Railroads
- Shipping
- Trains
- Supply Chain
- Logistics
- Spectral
- Linting
- API Governance
---
