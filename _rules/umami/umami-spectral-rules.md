---
api_specs:
- filename: umami-openapi.yml
  format: yaml
  label: Umami API
  slug: umami-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/umami/refs/heads/main/openapi/umami-openapi.yml
categories:
- analytics
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Umami.
layout: rules
name: Umami API Rules
provider_name: Umami
provider_slug: umami
rule_count: 31
rules:
- description: API title must start with "Umami"
  given: $.info.title
  name: info-title-umami-prefix
  severity: error
- description: API info must have a description with at least 50 characters
  given: $.info.description
  name: info-description-required
  severity: error
- description: API info must include a version
  given: $.info.version
  name: info-version-required
  severity: error
- description: API contact should include URL pointing to umami.is
  given: $.info.contact.url
  name: info-contact-url
  severity: warn
- description: OpenAPI version must be 3.0.x
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: At least one server must be defined
  given: $.servers
  name: servers-required
  severity: error
- description: Server URL should use umami.is domain or localhost for self-hosted
  given: $.servers[*].url
  name: servers-umami-domain
  severity: info
- description: All paths should start with /api/
  given: $.paths[*]~
  name: paths-api-prefix
  severity: info
- description: Paths must not have a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId-required
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summary must start with "Umami"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-umami-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: OperationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Query parameter names should use camelCase
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-camelCase
  severity: info
- description: Timestamp parameters should indicate millisecond precision in their names or descriptions
  given: $.paths[*][get].parameters[?(@.name == 'startAt' || @.name == 'endAt')]
  name: parameter-timestamps-ms
  severity: info
- description: Request body should include application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json
  severity: warn
- description: Every operation must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should have types defined
  given: $.components.schemas[*].properties[*]
  name: schema-property-type
  severity: warn
- description: ID fields should use format uuid
  given: $.components.schemas[*].properties[?(@.description =~ /identifier/i)].format
  name: schema-uuid-format
  severity: info
- description: Security schemes must be defined in components
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: Global security should be defined
  given: $.security
  name: security-global-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Analytics operations should accept startAt and endAt timestamp parameters
  given: $.paths[*][get].parameters[*].name
  name: analytics-timestamps-required
  severity: info
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
rules_file: rules/umami-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/umami/refs/heads/main/rules/umami-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 7
  warn: 11
slug: umami-spectral-rules
source_filename: umami-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # ============================================================\n  # INFO / METADATA\n  # ============================================================\n  info-title-umami-prefix:\n    description: API title must start with \"Umami\"\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Umami\"\n\n  info-description-required:\n    description: API info must have a description with at least 50 characters\n    severity: error\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API info must include a version\n    severity: error\n    given: $.info.version\n    then:\n      function: truthy\n\n  info-contact-url:\n    description: API contact should include URL pointing to umami.is\n    severity: warn\n    given: $.info.contact.url\n    then:\n      function: truthy\n\n  # ============================================================\n\
  \  # OPENAPI VERSION\n  # ============================================================\n  openapi-version-3:\n    description: OpenAPI version must be 3.0.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # ============================================================\n  # SERVERS\n  # ============================================================\n  servers-required:\n    description: At least one server must be defined\n    severity: error\n    given: $.servers\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  servers-umami-domain:\n    description: Server URL should use umami.is domain or localhost for self-hosted\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(umami\\\\.is|localhost)\"\n\n  # ============================================================\n  # PATHS — NAMING CONVENTIONS\n\
  \  # ============================================================\n  paths-api-prefix:\n    description: All paths should start with /api/\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  paths-kebab-case:\n    description: Path segments should use kebab-case\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_[a-z]\"\n\n  # ============================================================\n  # OPERATIONS\n  # ============================================================\n  operation-operationId-required:\n    description: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n\
  \    then:\n      field: operationId\n      function: truthy\n\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-umami-prefix:\n    description: Operation summary must start with \"Umami\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Umami\"\n\n  operation-description-required:\n    description: Every operation must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-operationId-camelCase:\n\
  \    description: OperationId must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ============================================================\n  # PARAMETERS\n  # ============================================================\n  parameter-description-required:\n    description: Every parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-camelCase:\n    description: Query parameter names should use camelCase\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  parameter-timestamps-ms:\n    description: Timestamp parameters should indicate millisecond\
  \ precision in their names or descriptions\n    severity: info\n    given: $.paths[*][get].parameters[?(@.name == 'startAt' || @.name == 'endAt')]\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n  # REQUEST BODIES\n  # ============================================================\n  request-body-json:\n    description: Request body should include application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  # ============================================================\n  # RESPONSES\n  # ============================================================\n  response-success-required:\n    description: Every operation must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n  \
  \      schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['202']\n            - required: ['204']\n\n  response-401-required:\n    description: Operations should define a 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n  # SCHEMAS\n  # ============================================================\n  schema-description-required:\n    description: Top-level schemas should have descriptions\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n    \
  \  function: truthy\n\n  schema-property-type:\n    description: Schema properties should have types defined\n    severity: warn\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-uuid-format:\n    description: ID fields should use format uuid\n    severity: info\n    given: $.components.schemas[*].properties[?(@.description =~ /identifier/i)].format\n    then:\n      function: pattern\n      functionOptions:\n        match: \"uuid\"\n\n  # ============================================================\n  # SECURITY\n  # ============================================================\n  security-schemes-defined:\n    description: Security schemes must be defined in components\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  security-global-required:\n    description: Global security should be defined\n    severity: warn\n    given: $.security\n    then:\n      function: truthy\n\
  \n  # ============================================================\n  # HTTP METHOD CONVENTIONS\n  # ============================================================\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # ============================================================\n  # ANALYTICS-SPECIFIC\n  # ============================================================\n  analytics-timestamps-required:\n    description: Analytics operations should accept startAt and endAt timestamp parameters\n    severity: info\n    given: $.paths[*][get].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(start_at|end_at|start_time|end_time)$\"\n\n  # ============================================================\n  # QUALITY\n  # ============================================================\n  no-empty-descriptions:\n\
  \    description: Descriptions must not be empty strings\n    severity: error\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/umami/refs/heads/main/rules/umami-spectral-rules.yml
tags:
- Cookieless Tracking
- Open Source
- Privacy
- Web Analytics
- Website Analytics
- Spectral
- Linting
- API Governance
---
