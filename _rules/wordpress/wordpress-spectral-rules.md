---
api_specs:
- filename: wordpress-rest-api-openapi.yml
  format: yaml
  label: WordPress REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wordpress/refs/heads/main/openapi/wordpress-rest-api-openapi.yml
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
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for WordPress.
layout: rules
name: WordPress API Rules
provider_name: WordPress
provider_slug: wordpress
rule_count: 41
rules:
- description: ''
  given: $.info.title
  name: info-title-wordpress-prefix
  severity: warn
- description: ''
  given: $.info
  name: info-description-required
  severity: error
- description: ''
  given: $.info
  name: info-version-required
  severity: error
- description: ''
  given: $.info
  name: info-contact-required
  severity: warn
- description: ''
  given: $.info
  name: info-license-required
  severity: warn
- description: ''
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: ''
  given: $
  name: servers-defined
  severity: error
- description: ''
  given: $.servers[*].url
  name: servers-https-only
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-version-prefix
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-wordpress-prefix
  severity: warn
- description: ''
  given: $
  name: tags-defined
  severity: info
- description: ''
  given: $.tags[*]
  name: tag-description-required
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameter-snake-case
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: info
- description: ''
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: ''
  given: $.paths[*][post,put,delete].responses
  name: response-401-for-auth
  severity: info
- description: ''
  given: $.paths[*~'\\{id\\}'][get].responses
  name: response-404-for-get-by-id
  severity: info
- description: ''
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: ''
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]
  name: schema-property-example
  severity: info
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: ''
  given: $.components.securitySchemes[*]
  name: security-scheme-description
  severity: warn
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
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-microcks-extension
  severity: info
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.paths[*][get].parameters[?(@.name == 'limit')]
  name: pagination-parameters-standard
  severity: info
rules_file: rules/wordpress-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wordpress/refs/heads/main/rules/wordpress-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 13
  warn: 18
slug: wordpress-spectral-rules
source_filename: wordpress-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-wordpress-prefix:\n    message: API title must begin with \"WordPress\"\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^WordPress'\n\n  info-description-required:\n    message: Info object must have a non-empty description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: Info object must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    message: Info object should have contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-license-required:\n    message: Info object should have license information\n    severity: warn\n    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  # OPENAPI\
  \ VERSION\n  openapi-version-3:\n    message: Must use OpenAPI 3.0.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: '^3\\.0\\.'\n\n  # SERVERS\n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    message: Path segments must use kebab-case\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z0-9{][a-z0-9\\-._{}]*)*$'\n\n  paths-no-trailing-slash:\n    message: Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n\
  \      functionOptions:\n        notMatch: '/$'\n\n  paths-version-prefix:\n    message: WordPress REST API paths should start with /wp/v2/\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/wp/v[0-9]+/'\n\n  # OPERATIONS\n  operation-summary-required:\n    message: Operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    message: Operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    message: Operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    message: operationId must use camelCase\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  operation-tags-required:\n    message: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-summary-wordpress-prefix:\n    message: Operation summaries must start with \"WordPress\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^WordPress'\n\n  # TAGS\n  tags-defined:\n    message: Global tags array must be defined\n    severity: info\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tag-description-required:\n    message: Tags must have a description\n    severity: info\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\
  \n  # PARAMETERS\n  parameter-description-required:\n    message: Parameters must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-snake-case:\n    message: Parameter names should use snake_case\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  parameter-schema-required:\n    message: Parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-description:\n    message: Request bodies should have a description\n    severity: info\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  request-body-json-content:\n \
  \   message: Request bodies should use application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    message: Operations must have a success response (2xx)\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-for-auth:\n    message: Authenticated endpoints should document 401 response\n    severity: info\n    given: $.paths[*][post,put,delete].responses\n\
  \    then:\n      field: '401'\n      function: truthy\n\n  response-404-for-get-by-id:\n    message: GET by ID endpoints should document 404 response\n    severity: info\n    given: $.paths[*~'\\\\{id\\\\}'][get].responses\n    then:\n      field: '404'\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    message: Top-level schemas must have a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-type-defined:\n    message: Schemas must have a type defined\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-property-snake-case:\n    message: Schema properties should use snake_case\n    severity: info\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  schema-property-description:\n    message:\
  \ Schema properties should have descriptions\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-property-example:\n    message: Schema properties should have examples\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: example\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    message: Security schemes must be defined in components\n    severity: warn\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-scheme-description:\n    message: Security schemes must have a description\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: description\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field:\
  \ requestBody\n      function: falsy\n\n  delete-no-request-body:\n    message: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  post-should-have-request-body:\n    message: POST operations creating resources should have a request body\n    severity: info\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  # MICROCKS COMPATIBILITY\n  operation-microcks-extension:\n    message: Operations should have x-microcks-operation extension for mock compatibility\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: '.+'\n\n  pagination-parameters-standard:\n\
  \    message: Pagination parameters should use page and per_page (WordPress convention)\n    severity: info\n    given: $.paths[*][get].parameters[?(@.name == 'limit')]\n    then:\n      function: undefined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wordpress/refs/heads/main/rules/wordpress-spectral-rules.yml
tags:
- CMS
- Content Management
- Open Source
- WordPress
- Spectral
- Linting
- API Governance
---
