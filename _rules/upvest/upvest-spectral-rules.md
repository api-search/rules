---
api_specs:
- filename: upvest-investment-api-openapi.yml
  format: yaml
  label: Upvest Investment API
  slug: investment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/openapi/upvest-investment-api-openapi.yml
categories:
- delete
- get
- info
- 'no'
- openapi
- operation
- pagination
- parameter
- paths
- post
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Upvest.
layout: rules
name: Upvest API Rules
provider_name: Upvest
provider_slug: upvest
rule_count: 39
rules:
- description: API title must start with "Upvest"
  given: $.info.title
  name: info-title-format
  severity: warn
- description: API must have a description with at least 50 characters
  given: $.info
  name: info-description-required
  severity: error
- description: API must define a version
  given: $.info
  name: info-version-required
  severity: error
- description: API info should include contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: All specs must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: API must define at least one server
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Each server must have a description
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments must use snake_case or kebab-case (Upvest uses snake_case)
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Upvest"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-upvest-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Tags used in operations should be defined at the global level
  given: $.tags
  name: tags-defined-globally
  severity: warn
- description: Global tags must have descriptions
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: error
- description: All parameters must have a schema
  given: $.paths[*][*].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Parameter names should use snake_case
  given: $.paths[*][*].parameters[*].name
  name: parameter-snake-case
  severity: warn
- description: Request bodies should have descriptions
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: POST/PUT/PATCH request bodies should support application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Every operation must have at least one success response (2xx)
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations using auth should define a 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Schema property names should use snake_case
  given: $.components.schemas[*].properties
  name: schema-properties-snake-case
  severity: warn
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schemas should define a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Schema id properties should use uuid format
  given: $.components.schemas[*].properties.id
  name: schema-id-uuid-format
  severity: info
- description: API must define security schemes
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: Global security must be defined
  given: $
  name: security-global-defined
  severity: warn
- description: OAuth2 scopes must have descriptions
  given: $.components.securitySchemes[*].flows[*].scopes
  name: security-oauth2-scopes-described
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: POST operations creating resources should have a request body
  given: $.paths[*].post
  name: post-should-have-request-body
  severity: warn
- description: Operations should have examples for better developer experience
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: operation-examples-encouraged
  severity: info
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Paginated operations should use offset/limit parameter names
  given: $.paths[*].get.parameters[*].name
  name: pagination-offset-limit
  severity: info
rules_file: rules/upvest-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/rules/upvest-spectral-rules.yml
severity_counts:
  error: 17
  hint: 0
  info: 3
  warn: 19
slug: upvest-spectral-rules
source_filename: upvest-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-format:\n    description: API title must start with \"Upvest\"\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Upvest\"\n\n  info-description-required:\n    description: API must have a description with at least 50 characters\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API must define a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: API info should include contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: All specs must use OpenAPI 3.x\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n    \
  \  function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: Each server must have a description\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use snake_case or kebab-case (Upvest uses snake_case)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z][a-z0-9_]*({[a-z][a-z0-9_]*})?)*$\"\n\n  paths-no-trailing-slash:\n\
  \    description: Paths must not end with a trailing slash\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-upvest-prefix:\n    description: Operation summaries must start with \"Upvest\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Upvest \"\n\n  operation-description-required:\n    description: Every operation must have a description\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: Every operation must\
  \ have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-defined-globally:\n    description: Tags used in operations should be defined at the global level\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n\n  tags-description-required:\n    description: Global tags must have descriptions\n    severity: warn\n    given: \"$.tags[*]\"\n    then:\n      field: description\n\
  \      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have descriptions\n    severity: error\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: All parameters must have a schema\n    severity: error\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  parameter-snake-case:\n    description: Parameter names should use snake_case\n    severity: warn\n    given: \"$.paths[*][*].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # REQUEST BODIES\n  request-body-description:\n    description: Request bodies should have descriptions\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  request-body-json-content:\n    description:\
  \ POST/PUT/PATCH request bodies should support application/json\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have at least one success response (2xx)\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: truthy\n\n  response-401-required:\n    description: Operations using auth should define a 401 response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  response-description-required:\n    description: All responses must have a description\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-properties-snake-case:\n    description: Schema property names should use\
  \ snake_case\n    severity: warn\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  schema-description-required:\n    description: Top-level schemas should have a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-type-defined:\n    description: Schemas should define a type\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  schema-id-uuid-format:\n    description: Schema id properties should use uuid format\n    severity: info\n    given: \"$.components.schemas[*].properties.id\"\n    then:\n      field: format\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: API must define security schemes\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\
  \n  security-global-defined:\n    description: Global security must be defined\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  security-oauth2-scopes-described:\n    description: OAuth2 scopes must have descriptions\n    severity: warn\n    given: \"$.components.securitySchemes[*].flows[*].scopes\"\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  post-should-have-request-body:\n    description: POST operations creating resources should have a request body\n    severity: warn\n    given: \"$.paths[*].post\"\n   \
  \ then:\n      field: requestBody\n      function: truthy\n\n  # GENERAL QUALITY\n  operation-examples-encouraged:\n    description: Operations should have examples for better developer experience\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*].content[*]\"\n    then:\n      field: examples\n      function: truthy\n\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: error\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^.{1,}\"\n\n  pagination-offset-limit:\n    description: Paginated operations should use offset/limit parameter names\n    severity: info\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - offset\n          - limit\n          - user_id\n          - account_id\n          - instrument_id\n          - order_id\n          - portfolio_id\n  \
  \        - savings_plan_id\n          - position_id\n          - webhook_id\n          - mandate_id\n          - file_id\n          - identifier_id\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/rules/upvest-spectral-rules.yml
tags:
- Banking Infrastructure
- Fintech
- Investments
- Securities
- Fractional Investing
- Custody
- Wealth Management
- Spectral
- Linting
- API Governance
---
