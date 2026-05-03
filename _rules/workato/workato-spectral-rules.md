---
api_specs:
- filename: workato-developer-api-openapi.yml
  format: yaml
  label: Workato
  slug: workato
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-developer-api-openapi.yml
- filename: workato-event-streams-openapi.yml
  format: yaml
  label: Workato Event Streams Public API
  slug: event-streams-public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-event-streams-openapi.yml
- filename: workato-mcp-server-openapi.yml
  format: yaml
  label: Workato MCP Server API
  slug: mcp-server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-mcp-server-openapi.yml
categories:
- delete
- get
- info
- microcks
- 'no'
- openapi
- operation
- operations
- parameter
- paths
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Workato.
layout: rules
name: Workato API Rules
provider_name: Workato
provider_slug: workato
rule_count: 38
rules:
- description: ''
  given: $.info.title
  name: info-title-workato-prefix
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
  severity: error
- description: ''
  given: $.servers[*].url
  name: servers-workato-domain
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: ''
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-api-prefix
  severity: warn
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
  name: operation-summary-workato-prefix
  severity: warn
- description: ''
  given: $
  name: tags-defined
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameter-snake-case
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
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-unauthorized
  severity: warn
- description: ''
  given: $.paths[*][post,put].responses
  name: response-422-validation
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
  severity: warn
- description: ''
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: error
- description: ''
  given: $.components.securitySchemes[*]
  name: security-bearer-token
  severity: warn
- description: ''
  given: $.components.securitySchemes[*][?(@.type == 'apiKey')]
  name: security-header-api-token
  severity: info
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: ''
  given: $.paths[*].delete.responses
  name: delete-returns-success
  severity: warn
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*].content.application\/json
  name: operations-have-examples
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
rules_file: rules/workato-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/rules/workato-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 8
  warn: 18
slug: workato-spectral-rules
source_filename: workato-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-workato-prefix:\n    message: API title must begin with \"Workato\"\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^Workato'\n\n  info-description-required:\n    message: Info object must have a non-empty description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: Info object must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    message: Info object should include contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    message: Must use OpenAPI 3.0.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ '^3\\.0\\.'\n\n  # SERVERS\n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  servers-workato-domain:\n    message: Server URLs should use the workato.com domain\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: 'workato\\.com'\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    message: Path segments must use kebab-case or snake_case (Workato uses snake_case)\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z0-9{][a-z0-9\\-._{}]*)*$'\n\n  paths-no-trailing-slash:\n    message: Paths must not have a trailing slash\n\
  \    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '/$'\n\n  paths-api-prefix:\n    message: Workato API paths should begin with /api/\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/api/'\n\n  # OPERATIONS\n  operation-summary-required:\n    message: All operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    message: All operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    message: All operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n\
  \  operation-id-camel-case:\n    message: operationId must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  operation-tags-required:\n    message: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-summary-workato-prefix:\n    message: Operation summaries must start with \"Workato\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^Workato'\n\n  # TAGS\n  tags-defined:\n    message: Global tags array should be defined\n    severity: info\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    message: Parameters must have a description\n    severity:\
  \ warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    message: Parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  parameter-snake-case:\n    message: Parameter names should use snake_case (Workato convention)\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  # REQUEST BODIES\n  request-body-json-content:\n    message: Request bodies should use application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    message: Operations must have a success response\
  \ (200 or 201)\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-unauthorized:\n    message: Authenticated endpoints must document 401 response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-422-validation:\n    message: POST/PUT endpoints should document 422 validation errors\n    severity: info\n    given: $.paths[*][post,put].responses\n    then:\n      field: '422'\n      function: truthy\n\n\
  \  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    message: Top-level schemas must have a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-type-defined:\n    message: Schemas must have a type defined\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-property-snake-case:\n    message: Schema properties should use snake_case (Workato convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  schema-property-description:\n    message: Schema properties should have descriptions\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    message: Security schemes must be\
  \ defined in components\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-bearer-token:\n    message: Workato APIs should use bearer token authentication\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: '^bearer$'\n\n  security-header-api-token:\n    message: API token should be in Authorization header as Bearer token\n    severity: info\n    given: $.components.securitySchemes[*][?(@.type == 'apiKey')]\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values: [header]\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-returns-success:\n    message: DELETE operations should return 200\
  \ or 204\n    severity: warn\n    given: $.paths[*].delete.responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['204']\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: '.+'\n\n  operations-have-examples:\n    message: Operations should have response examples for documentation and mocking\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].responses[*].content.application\\/json\n    then:\n      field: examples\n      function: truthy\n\n  microcks-operation-extension:\n    message: Operations should have x-microcks-operation extension for mock server compatibility\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n\
  \      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/rules/workato-spectral-rules.yml
tags:
- Agentic
- API Management
- Automation
- B2B
- Embedded iPaaS
- Enterprise
- Integration
- iPaaS
- Orchestration
- Workflow
- Spectral
- Linting
- API Governance
---
