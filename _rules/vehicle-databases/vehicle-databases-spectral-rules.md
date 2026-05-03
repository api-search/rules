---
api_specs:
- filename: vehicle-databases-openapi.yml
  format: yaml
  label: Vehicle Databases Maintenance API
  slug: vehicle-databases
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vehicle-databases/refs/heads/main/openapi/vehicle-databases-openapi.yml
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
description: Spectral linting rules defining API design standards and conventions for Vehicle Databases.
layout: rules
name: Vehicle Databases API Rules
provider_name: Vehicle Databases
provider_slug: vehicle-databases
rule_count: 21
rules:
- description: Info title must be defined.
  given: $.info
  name: info-title-required
  severity: error
- description: Info description must be non-empty.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be defined.
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Path segments should use kebab-case.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Vehicle Databases".
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-operationid-camelcase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: All parameters must have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Operations with path parameters should define 404 responses.
  given: $.paths[*][get].responses
  name: response-404-defined
  severity: warn
- description: Component schemas must have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Security schemes must be defined.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: API key authentication should use header placement (X-API-Key).
  given: $.components.securitySchemes[?(@.type == 'apiKey')]
  name: security-apikey-header
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/vehicle-databases-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vehicle-databases/refs/heads/main/rules/vehicle-databases-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 1
  warn: 10
slug: vehicle-databases-spectral-rules
source_filename: vehicle-databases-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO\n  info-title-required:\n    description: Info title must be defined.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info description must be non-empty.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be defined.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: Must use OpenAPI 3.x.\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n\
  \    description: Server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS\n  paths-kebab-case:\n    description: Path segments should use kebab-case.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_/-]+)+$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-prefix:\n    description: Operation summaries must start with \"Vehicle Databases\".\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Vehicle Databases \"\n\n  operation-description-required:\n    description:\
  \ Every operation must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camelcase:\n    description: operationId must use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have\
  \ a description.\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have a 2xx response.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  response-404-defined:\n    description: Operations with path parameters should define 404 responses.\n    severity: warn\n    given: \"$.paths[*][get].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"404\"]\n\n  # SCHEMAS\n  schema-description-required:\n    description: Component schemas must have descriptions.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field:\
  \ description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined.\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-apikey-header:\n    description: API key authentication should use header placement (X-API-Key).\n    severity: info\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')]\"\n    then:\n      field: in\n      function: pattern\n      functionOptions:\n        match: \"^header$\"\n\n  # HTTP METHODS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL\n  no-empty-descriptions:\n    description: Descriptions must not be empty.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vehicle-databases/refs/heads/main/rules/vehicle-databases-spectral-rules.yml
tags:
- Automotive
- Fleet Management
- Maintenance
- Recalls
- Vehicles
- Spectral
- Linting
- API Governance
---
