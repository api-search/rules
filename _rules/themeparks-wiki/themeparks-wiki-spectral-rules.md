---
api_specs:
- filename: themeparks-wiki-openapi.yml
  format: yaml
  label: ThemeParks.wiki API
  slug: themeparks-wiki
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/themeparks-wiki/refs/heads/main/openapi/themeparks-wiki-openapi.yml
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
description: Spectral linting rules defining API design standards and conventions for ThemeParks.wiki.
layout: rules
name: ThemeParks.wiki API Rules
provider_name: ThemeParks.wiki
provider_slug: themeparks-wiki
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
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
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
- description: Operation summaries should start with 'ThemeParks.wiki'
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-provider-prefix
  severity: info
- description: Entity ID path parameters should use UUID format
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='entityID')]
  name: parameter-entity-id-uuid
  severity: info
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must have at least one success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Entity endpoints should document 404 not found response
  given: $.paths[/entity/*][get].responses
  name: response-404-for-entity-paths
  severity: warn
- description: Response objects must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schema objects should have a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: ThemeParks.wiki API requires no authentication
  given: $
  name: no-auth-required
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/themeparks-wiki-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/themeparks-wiki/refs/heads/main/rules/themeparks-wiki-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 3
  warn: 11
slug: themeparks-wiki-spectral-rules
source_filename: themeparks-wiki-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be defined\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: OpenAPI version should be 3.x\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: Servers array must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n\
  \    description: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS\n  paths-kebab-case:\n    description: Path segments must use kebab-case\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9]+(-[a-z0-9]+)*(/{[a-zA-Z]+})?)*$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    description: Operations must have a description\n    severity: warn\n    given:\
  \ $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  operation-operationId-required:\n    description: Operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  operation-summary-provider-prefix:\n    description: Operation summaries should start with 'ThemeParks.wiki'\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^ThemeParks.wiki \"\n\n  # PARAMETERS\n  parameter-entity-id-uuid:\n    description: Entity ID path parameters should use UUID format\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='entityID')]\n\
  \    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - uuid\n\n  parameter-description-required:\n    description: Parameters must have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must have at least one success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-404-for-entity-paths:\n    description: Entity endpoints should document 404 not found response\n    severity: warn\n    given: $.paths[/entity/*][get].responses\n    then:\n      field: \"404\"\n      function: defined\n\n  response-description-required:\n    description: Response objects must have\
  \ a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-type-defined:\n    description: Schema objects should have a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # SECURITY\n  no-auth-required:\n    description: ThemeParks.wiki API requires no authentication\n    severity: info\n    given: $\n    then:\n      field: security\n      function: falsy\n\n  # HTTP METHODS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/themeparks-wiki/refs/heads/main/rules/themeparks-wiki-spectral-rules.yml
tags:
- Entertainment
- Real-Time
- Theme Parks
- Wait Times
- Travel
- Spectral
- Linting
- API Governance
---
