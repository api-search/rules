---
api_specs:
- filename: themealdb-openapi.yml
  format: yaml
  label: TheMealDB API
  slug: themealdb
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/themealdb/refs/heads/main/openapi/themealdb-openapi.yml
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for TheMealDB.
layout: rules
name: TheMealDB API Rules
provider_name: TheMealDB
provider_slug: themealdb
rule_count: 18
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
- description: Operation summaries should start with 'TheMealDB'
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-provider-prefix
  severity: info
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must have a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Response objects must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
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
- description: Operations should have examples
  given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]
  name: operation-examples-encouraged
  severity: info
rules_file: rules/themealdb-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/themealdb/refs/heads/main/rules/themealdb-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 8
slug: themealdb-spectral-rules
source_filename: themealdb-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be defined\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: OpenAPI version should be 3.x\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: Servers array must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n\
  \    description: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    description: Operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  operation-operationId-required:\n    description: Operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n\
  \    then:\n      field: tags\n      function: truthy\n\n  operation-summary-provider-prefix:\n    description: Operation summaries should start with 'TheMealDB'\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^TheMealDB \"\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Parameters must have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must have a success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-description-required:\n    description: Response objects must have a description\n    severity:\
  \ warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-type-defined:\n    description: Schema objects should have a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # HTTP METHODS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  operation-examples-encouraged:\n    description: Operations should have examples\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]\n    then:\n      field: examples\n      function:\
  \ defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/themealdb/refs/heads/main/rules/themealdb-spectral-rules.yml
tags:
- Recipes
- Meals
- Food
- Cooking
- Spectral
- Linting
- API Governance
---
