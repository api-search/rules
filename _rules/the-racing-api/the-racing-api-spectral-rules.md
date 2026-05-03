---
api_specs:
- filename: the-racing-api-openapi.yml
  format: yaml
  label: The Racing API
  slug: the-racing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-racing-api/refs/heads/main/openapi/the-racing-api-openapi.yml
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
- security
- servers
description: Spectral linting rules defining API design standards and conventions for The Racing API.
layout: rules
name: The Racing API API Rules
provider_name: The Racing API
provider_slug: the-racing-api
rule_count: 28
rules:
- description: Info object must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info object must have a description with minimum length
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be defined
  given: $.info
  name: info-version-required
  severity: error
- description: OpenAPI version should be 3.1.x
  given: $
  name: openapi-version-31
  severity: warn
- description: Servers array must be defined and non-empty
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Paths should include version prefix /v1/
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
- description: Operation summaries should start with 'The Racing API'
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-provider-prefix
  severity: info
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Query parameter names should use snake_case
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in=='query')].name
  name: parameter-snake-case
  severity: info
- description: API keys should be in headers not query parameters
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='api_key' || @.name=='apikey')]
  name: parameter-apikey-not-in-query
  severity: warn
- description: Operations must have at least one 2xx response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Response objects must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Endpoints with path parameters should have a 404 response
  given: $.paths[~*{*}*][get].responses
  name: response-404-for-id-paths
  severity: info
- description: The Racing API uses 422 for validation errors
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-422-validation-error
  severity: info
- description: Schema objects should have a type defined
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Security schemes must be defined in components
  given: $.components
  name: security-schemes-defined
  severity: error
- description: The Racing API uses HTTP Basic authentication
  given: $.components.securitySchemes[*]
  name: security-basic-auth
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Operations should have examples for mock server compatibility
  given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]
  name: operation-examples-encouraged
  severity: info
rules_file: rules/the-racing-api-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-racing-api/refs/heads/main/rules/the-racing-api-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 8
  warn: 11
slug: the-racing-api-spectral-rules
source_filename: the-racing-api-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info object must have a description with minimum length\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        value: 20\n\n  info-version-required:\n    description: API version must be defined\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-31:\n    description: OpenAPI version should be 3.1.x\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: Servers array must be defined and non-empty\n    severity: error\n  \
  \  given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9]+)?(/[a-z0-9]+(-[a-z0-9]+)*(/{[a-z_]+})?)*$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-versioned:\n    description: Paths should include version prefix /v1/\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]\"\n\n  # OPERATIONS\n\
  \  operation-summary-required:\n    description: Operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    description: Operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  operation-operationId-required:\n    description: Operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  operation-summary-provider-prefix:\n    description: Operation summaries should start with 'The Racing API'\n    severity: info\n   \
  \ given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^The Racing API \"\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Parameters must have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-snake-case:\n    description: Query parameter names should use snake_case\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in=='query')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  parameter-apikey-not-in-query:\n    description: API keys should be in headers not query parameters\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='api_key' || @.name=='apikey')]\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n\
  \        values:\n          - header\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must have at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-description-required:\n    description: Response objects must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-404-for-id-paths:\n    description: Endpoints with path parameters should have a 404 response\n    severity: info\n    given: $.paths[~*{*}*][get].responses\n    then:\n      field: \"404\"\n      function: truthy\n\n  response-422-validation-error:\n    description: The Racing API uses 422 for validation errors\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].responses\n\
  \    then:\n      field: \"422\"\n      function: defined\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-type-defined:\n    description: Schema objects should have a type defined\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-description-required:\n    description: Top-level schemas should have a description\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-basic-auth:\n    description: The Racing API uses HTTP Basic authentication\n    severity: info\n    given: $.components.securitySchemes[*]\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n\n  # HTTP\
  \ METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  operation-examples-encouraged:\n    description: Operations should have examples for mock server compatibility\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]\n    then:\n      field: examples\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-racing-api/refs/heads/main/rules/the-racing-api-spectral-rules.yml
tags:
- Horse Racing
- Sports
- Statistics
- Betting
- Analytics
- Spectral
- Linting
- API Governance
---
