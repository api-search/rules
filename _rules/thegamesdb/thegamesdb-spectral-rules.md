---
api_specs:
- filename: thegamesdb-openapi.yml
  format: yaml
  label: TheGamesDB API
  slug: thegamesdb
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thegamesdb/refs/heads/main/openapi/thegamesdb-openapi.yml
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for TheGamesDB.
layout: rules
name: TheGamesDB API Rules
provider_name: TheGamesDB
provider_slug: thegamesdb
rule_count: 22
rules:
- description: Info object must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info object must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be defined
  given: $.info
  name: info-version-required
  severity: error
- description: OpenAPI version should be 3.x
  given: $
  name: openapi-version-3
  severity: warn
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Paths should include a version prefix
  given: $.paths[*]~
  name: paths-versioned
  severity: info
- description: Operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operations must have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Operation summaries should start with 'TheGamesDB'
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-provider-prefix
  severity: info
- description: TheGamesDB requires apikey query parameter on all operations
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='apikey')]
  name: parameter-apikey-required-in-query
  severity: warn
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Paginated endpoints should use 'page' parameter name
  given: $.paths[*][get].parameters[?(@.name=='offset')]
  name: parameter-pagination-page
  severity: info
- description: Operations must have at least one success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Query endpoints should document 400 bad input response
  given: $.paths[*][get].responses
  name: response-400-for-query-endpoints
  severity: info
- description: TheGamesDB endpoints should document 403 invalid key response
  given: $.paths[*][get].responses
  name: response-403-for-api-key
  severity: warn
- description: Schema objects should have a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/thegamesdb-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thegamesdb/refs/heads/main/rules/thegamesdb-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 4
  warn: 10
slug: thegamesdb-spectral-rules
source_filename: thegamesdb-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be defined\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: OpenAPI version should be 3.x\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: Servers array must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n\
  \    description: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-versioned:\n    description: Paths should include a version prefix\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    description: Operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n\
  \    then:\n      field: description\n      function: truthy\n\n  operation-operationId-required:\n    description: Operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  operation-summary-provider-prefix:\n    description: Operation summaries should start with 'TheGamesDB'\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^TheGamesDB \"\n\n  # PARAMETERS\n  parameter-apikey-required-in-query:\n    description: TheGamesDB requires apikey query parameter on all operations\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='apikey')]\n\
  \    then:\n      field: required\n      function: truthy\n\n  parameter-description-required:\n    description: Parameters must have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-pagination-page:\n    description: Paginated endpoints should use 'page' parameter name\n    severity: info\n    given: $.paths[*][get].parameters[?(@.name=='offset')]\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must have at least one success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-400-for-query-endpoints:\n    description: Query endpoints should document\
  \ 400 bad input response\n    severity: info\n    given: $.paths[*][get].responses\n    then:\n      field: \"400\"\n      function: defined\n\n  response-403-for-api-key:\n    description: TheGamesDB endpoints should document 403 invalid key response\n    severity: warn\n    given: $.paths[*][get].responses\n    then:\n      field: \"403\"\n      function: defined\n\n  # SCHEMAS\n  schema-type-defined:\n    description: Schema objects should have a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # HTTP METHODS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thegamesdb/refs/heads/main/rules/thegamesdb-spectral-rules.yml
tags:
- Database
- Gaming
- Video Games
- Metadata
- Artwork
- Spectral
- Linting
- API Governance
---
