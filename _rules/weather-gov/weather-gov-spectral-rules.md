---
api_specs:
- filename: openapi.yml
  format: yaml
  label: Weather.gov API Web Service
  slug: weather-gov-api-web-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weather-gov/refs/heads/main/openapi/openapi.yml
categories:
- contact
- delete
- external
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
description: Spectral linting rules defining API design standards and conventions for Weather.gov.
layout: rules
name: Weather.gov API Rules
provider_name: Weather.gov
provider_slug: weather-gov
rule_count: 24
rules:
- description: Info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers array must be defined
  given: $
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: OperationId must use snake_case
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-operationId-snake-case
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have tags
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Every operation must have a 2xx success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schema properties must define a type
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: Schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
- description: Security schemes must be defined in components
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Info should have contact details
  given: $.info
  name: contact-info-recommended
  severity: info
- description: Spec should have external documentation link
  given: $
  name: external-docs-recommended
  severity: info
rules_file: rules/weather-gov-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/weather-gov/refs/heads/main/rules/weather-gov-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 3
  warn: 13
slug: weather-gov-spectral-rules
source_filename: weather-gov-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info must have a title\n    message: OpenAPI spec must have a title in info\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info must have a description\n    message: OpenAPI spec must have a description in info\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: Info must have a version\n    message: OpenAPI spec must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: Must use OpenAPI 3.x\n    message: Spec must use OpenAPI 3.0.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # SERVERS\n\
  \  servers-required:\n    description: Servers array must be defined\n    message: Spec must define servers\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS\n    message: Server URL must use HTTPS\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segments must be kebab-case: {{value}}\"\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}_,\\\\-\\\\/]*)*$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: \"Path must not end with a trailing slash: {{value}}\"\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  # OPERATIONS\n  operation-operationId-required:\n    description: Every operation must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-snake-case:\n    description: OperationId must use snake_case\n    message: \"OperationId must use snake_case: {{value}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  operation-description-required:\n    description: Every operation must have a description\n    message: Operation must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description:\
  \ Every operation must have tags\n    message: Operation must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter must have a description\n    message: Parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: Every parameter must have a schema\n    message: Parameter must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have a 2xx success response\n    message: Operation must define at least one 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          minProperties: 1\n\n  response-description-required:\n    description: Every response must have a description\n    message: Response must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-type-required:\n    description: Schema properties must define a type\n    message: Schema must have a type defined\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-description-recommended:\n    description: Schemas should have descriptions\n    message: Schema should have a description\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components\n\
  \    message: API must define security schemes\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    message: GET operation must not have a requestBody\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    message: DELETE operation should not have a requestBody\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    message: Description must not be empty\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  contact-info-recommended:\n\
  \    description: Info should have contact details\n    message: Info should include contact information\n    severity: info\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  external-docs-recommended:\n    description: Spec should have external documentation link\n    message: Spec should include externalDocs\n    severity: info\n    given: $\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/weather-gov/refs/heads/main/rules/weather-gov-spectral-rules.yml
tags:
- Weather
- Government
- United States
- Forecasting
- Alerts
- Open Data
- Spectral
- Linting
- API Governance
---
