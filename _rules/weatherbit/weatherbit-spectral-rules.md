---
api_specs:
- filename: weatherbit-current-weather-openapi-original.yml
  format: yaml
  label: Weatherbit Current Weather API
  slug: weatherbit-current-weather-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weatherbit/refs/heads/main/openapi/weatherbit-current-weather-openapi-original.yml
categories:
- contact
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
description: Spectral linting rules defining API design standards and conventions for Weatherbit.
layout: rules
name: Weatherbit API Rules
provider_name: Weatherbit
provider_slug: weatherbit
rule_count: 19
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
- description: Path segments must use kebab-case or snake_case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: warn
- description: Operation summaries must start with Weatherbit
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-weatherbit-prefix
  severity: info
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Every parameter should have a description
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: API key parameter must be named 'key'
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name == 'key')]
  name: parameter-api-key-in-query
  severity: info
- description: Every operation must have a 2xx success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schemas should define a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Info should have contact details
  given: $.info
  name: contact-info-recommended
  severity: info
rules_file: rules/weatherbit-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/weatherbit/refs/heads/main/rules/weatherbit-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 4
  warn: 9
slug: weatherbit-spectral-rules
source_filename: weatherbit-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: Info must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: Must use OpenAPI 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers array must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All\
  \ server URLs must use HTTPS\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case or snake_case\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}_,\\\\-\\\\/]*)*$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-weatherbit-prefix:\n    description: Operation summaries must start with Weatherbit\n\
  \    message: \"Summary must start with 'Weatherbit': {{value}}\"\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Weatherbit\"\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-api-key-in-query:\n    description: API key parameter must be named 'key'\n    message: \"API key parameter should be named 'key'\"\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name == 'key')]\n    then:\n      field: in\n      function: enumeration\n\
  \      functionOptions:\n        values: [query]\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have a 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          minProperties: 1\n\n  response-description-required:\n    description: Every response must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-type-defined:\n    description: Schemas should define a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function:\
  \ falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  contact-info-recommended:\n    description: Info should have contact details\n    severity: info\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/weatherbit/refs/heads/main/rules/weatherbit-spectral-rules.yml
tags:
- Weather
- Forecasting
- Historical Data
- Air Quality
- Alerts
- Agricultural Weather
- Spectral
- Linting
- API Governance
---
