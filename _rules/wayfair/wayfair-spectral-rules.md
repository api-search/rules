---
api_specs:
- filename: wayfair-supplier-api.yml
  format: yaml
  label: Wayfair Supplier API
  slug: wayfair-supplier-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wayfair/refs/heads/main/openapi/wayfair-supplier-api.yml
categories:
- get
- graphql
- info
- microcks
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
- servers
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for Wayfair.
layout: rules
name: Wayfair API Rules
provider_name: Wayfair
provider_slug: wayfair
rule_count: 31
rules:
- description: Info title must be present and non-empty.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Wayfair".
  given: $.info
  name: info-title-prefix
  severity: warn
- description: Info description must be present and at least 50 characters.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be defined.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information should be provided.
  given: $.info
  name: info-contact-required
  severity: warn
- description: OpenAPI version must be 3.1.x.
  given: $
  name: openapi-version
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Path segments must use kebab-case or standard REST conventions.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Wayfair".
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-title-case
  severity: warn
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Global tags array should be defined.
  given: $
  name: tags-defined
  severity: warn
- description: Every tag should have a description.
  given: $.tags[*]
  name: tag-description
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete][parameters][*]
  name: parameter-description-required
  severity: error
- description: POST operations should have a request body.
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: Request bodies should specify application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Every operation must have at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: GraphQL endpoint must define a 401 response.
  given: $.paths[/graphql].post
  name: response-401-graphql
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GraphQL endpoint must declare security.
  given: $.paths[/graphql].post
  name: graphql-security-required
  severity: error
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Operations should include x-microcks-operation for mock support.
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
rules_file: rules/wayfair-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wayfair/refs/heads/main/rules/wayfair-spectral-rules.yml
severity_counts:
  error: 14
  hint: 0
  info: 1
  warn: 16
slug: wayfair-spectral-rules
source_filename: wayfair-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: Info title must be present and non-empty.\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-title-prefix:\n    description: API title should start with \"Wayfair\".\n    severity: warn\n    given: $.info\n    then:\n      field: title\n      function: pattern\n      functionOptions:\n        match: '^Wayfair'\n\n  info-description-required:\n    description: Info description must be present and at least 50 characters.\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        value: 50\n\n  info-version-required:\n    description: API version must be defined.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information should be provided.\n    severity: warn\n    given: $.info\n\
  \    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version:\n    description: OpenAPI version must be 3.1.x.\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: '^3\\.1\\.'\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  servers-description:\n    description: Each server should have a description.\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case or standard\
  \ REST conventions.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z0-9{}-]+)+$'\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '/$'\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries should start with \"Wayfair\".\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: pattern\n      functionOptions:\n        match: '^Wayfair '\n\n  operation-description-required:\n    description: Every operation should have\
  \ a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: operationId must use camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-defined:\n    description: Global tags array should be defined.\n   \
  \ severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tag-description:\n    description: Every tag should have a description.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete][parameters][*]\n    then:\n      field: description\n      function: truthy\n\n  # REQUEST BODIES\n  post-has-request-body:\n    description: POST operations should have a request body.\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  request-body-json-content:\n    description: Request bodies should specify application/json content type.\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n\
  \  # RESPONSES\n  response-success-required:\n    description: Every operation must have at least one 2xx response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-401-graphql:\n    description: GraphQL endpoint must define a 401 response.\n    severity: warn\n    given: $.paths[/graphql].post\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '401'\n\n  response-description-required:\n    description: Every response must have a description.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description: Top-level schemas should have\
  \ a description.\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  graphql-security-required:\n    description: GraphQL endpoint must declare security.\n    severity: error\n    given: $.paths[/graphql].post\n    then:\n      field: security\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings.\n    severity: error\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: '.+'\n\n  microcks-operation-extension:\n    description: Operations should include x-microcks-operation for mock support.\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wayfair/refs/heads/main/rules/wayfair-spectral-rules.yml
tags:
- E-Commerce
- Furniture
- Home Goods
- Retail
- Suppliers
- GraphQL
- Spectral
- Linting
- API Governance
---
