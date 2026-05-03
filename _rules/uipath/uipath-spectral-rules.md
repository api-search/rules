---
api_specs:
- filename: uipath-orchestrator-openapi.yml
  format: yaml
  label: UiPath Orchestrator API
  slug: uipath-orchestrator-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-orchestrator-openapi.yml
- filename: uipath-automation-hub-openapi.yml
  format: yaml
  label: UiPath Automation Hub API
  slug: uipath-automation-hub-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-automation-hub-openapi.yml
- filename: uipath-document-understanding-openapi.yml
  format: yaml
  label: UiPath Document Understanding API
  slug: uipath-document-understanding-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-document-understanding-openapi.yml
- filename: uipath-data-service-openapi.yml
  format: yaml
  label: UiPath Data Service API
  slug: uipath-data-service-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-data-service-openapi.yml
- filename: uipath-platform-management-openapi.yml
  format: yaml
  label: UiPath Platform Management API
  slug: uipath-platform-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-platform-management-openapi.yml
- filename: uipath-test-manager-openapi.yml
  format: yaml
  label: UiPath Test Manager API
  slug: uipath-test-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-test-manager-openapi.yml
categories:
- delete
- external
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
- tags
description: Spectral linting rules defining API design standards and conventions for UiPath.
layout: rules
name: UiPath API Rules
provider_name: UiPath
provider_slug: uipath
rule_count: 40
rules:
- description: API title must be present and start with "UiPath"
  given: $.info.title
  name: info-title-required
  severity: error
- description: API info must have a description with at least 50 characters
  given: $.info.description
  name: info-description-required
  severity: error
- description: API info must include a version
  given: $.info.version
  name: info-version-required
  severity: error
- description: API contact should include a URL
  given: $.info.contact.url
  name: info-contact-url
  severity: warn
- description: API should reference UiPath terms of service
  given: $.info.termsOfService
  name: info-terms-of-service
  severity: warn
- description: OpenAPI version must be 3.0.x or 3.1.x
  given: $.openapi
  name: openapi-version
  severity: error
- description: At least one server must be defined
  given: $.servers
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Each server should have a description
  given: $.servers[*].description
  name: servers-description
  severity: warn
- description: Path segments must use kebab-case (no underscores or camelCase)
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Paths must not contain query strings
  given: $.paths[*]~
  name: paths-no-query-string
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationId-required
  severity: error
- description: OperationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summary must start with "UiPath"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-uipath-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: OperationId should start with a standard verb (list, get, create, update, delete, add, remove, search, run, upload)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-verb-prefix
  severity: info
- description: Global tags array should be defined
  given: $.tags
  name: tags-global-defined
  severity: warn
- description: All tags should have descriptions
  given: $.tags[*].description
  name: tags-description
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter schema must have a type defined
  given: $.paths[*][get,post,put,patch,delete].parameters[*].schema
  name: parameter-schema-type
  severity: warn
- description: Pagination size parameter should be named 'pageSize' (not 'limit' or 'size')
  given: $.paths[*][get].parameters[*]
  name: parameter-pagination-pageSize
  severity: info
- description: API keys should be passed in headers, not query parameters
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'api_key' || @.name == 'apiKey' || @.name == 'access_token')]
  name: parameter-no-api-key-in-query
  severity: error
- description: Request body should include application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Request body should have a description
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: info
- description: Every operation must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-error-401
  severity: warn
- description: Operations with request bodies should define a 400 Bad Request response
  given: $.paths[*][post,put,patch].responses
  name: response-error-400
  severity: warn
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description
  severity: warn
- description: Schema properties should have a type defined
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
- description: Schema property names should use camelCase
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camelCase
  severity: info
- description: Security schemes should be defined in components
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: warn
- description: Global security should be defined at the spec level
  given: $.security
  name: security-global-defined
  severity: warn
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: API spec should include externalDocs pointing to documentation
  given: $.externalDocs
  name: external-docs-encouraged
  severity: info
rules_file: rules/uipath-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/rules/uipath-spectral-rules.yml
severity_counts:
  error: 15
  hint: 0
  info: 5
  warn: 20
slug: uipath-spectral-rules
source_filename: uipath-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # ============================================================\n  # INFO / METADATA\n  # ============================================================\n  info-title-required:\n    description: API title must be present and start with \"UiPath\"\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^UiPath\"\n\n  info-description-required:\n    description: API info must have a description with at least 50 characters\n    severity: error\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API info must include a version\n    severity: error\n    given: $.info.version\n    then:\n      function: truthy\n\n  info-contact-url:\n    description: API contact should include a URL\n    severity: warn\n    given: $.info.contact.url\n    then:\n      function: truthy\n\n  info-terms-of-service:\n    description:\
  \ API should reference UiPath terms of service\n    severity: warn\n    given: $.info.termsOfService\n    then:\n      function: truthy\n\n  # ============================================================\n  # OPENAPI VERSION\n  # ============================================================\n  openapi-version:\n    description: OpenAPI version must be 3.0.x or 3.1.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.(0|1)\\\\.\"\n\n  # ============================================================\n  # SERVERS\n  # ============================================================\n  servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: $.servers\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  servers-https:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^https://\"\n\n  servers-description:\n    description: Each server should have a description\n    severity: warn\n    given: $.servers[*].description\n    then:\n      function: truthy\n\n  # ============================================================\n  # PATHS — NAMING CONVENTIONS\n  # ============================================================\n  paths-kebab-case:\n    description: Path segments must use kebab-case (no underscores or camelCase)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_[a-z]|[a-z][A-Z]\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  paths-no-query-string:\n    description: Paths must not contain query strings\n    severity: error\n    given: $.paths[*]~\n    then:\n\
  \      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  # ============================================================\n  # OPERATIONS\n  # ============================================================\n  operation-operationId-required:\n    description: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camelCase:\n    description: OperationId must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-uipath-prefix:\n\
  \    description: Operation summary must start with \"UiPath\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^UiPath\"\n\n  operation-description-required:\n    description: Every operation must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-operationId-verb-prefix:\n    description: OperationId should start with a standard verb (list, get, create, update, delete, add, remove, search, run, upload)\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^(list|get|create|update|delete|add|remove|search|run|upload|submit|validate|execute|process|start|stop|cancel|manage)\"\n\n  # ============================================================\n  # TAGS\n  # ============================================================\n  tags-global-defined:\n    description: Global tags array should be defined\n    severity: warn\n    given: $.tags\n    then:\n      function: truthy\n\n  tags-description:\n    description: All tags should have descriptions\n    severity: warn\n    given: $.tags[*].description\n    then:\n      function: truthy\n\n  # ============================================================\n  # PARAMETERS\n  # ============================================================\n  parameter-description-required:\n    description: Every parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-type:\n\
  \    description: Every parameter schema must have a type defined\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*].schema\n    then:\n      field: type\n      function: truthy\n\n  parameter-pagination-pageSize:\n    description: Pagination size parameter should be named 'pageSize' (not 'limit' or 'size')\n    severity: info\n    given: $.paths[*][get].parameters[*]\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(limit|page_size|size)$\"\n\n  parameter-no-api-key-in-query:\n    description: API keys should be passed in headers, not query parameters\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'api_key' || @.name == 'apiKey' || @.name == 'access_token')]\n    then:\n      field: in\n      function: pattern\n      functionOptions:\n        notMatch: \"^query$\"\n\n  # ============================================================\n  # REQUEST BODIES\n  # ============================================================\n\
  \  request-body-json-content:\n    description: Request body should include application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-description:\n    description: Request body should have a description\n    severity: info\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n  # RESPONSES\n  # ============================================================\n  response-success-required:\n    description: Every operation must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n           \
  \ - required: ['202']\n            - required: ['204']\n\n  response-error-401:\n    description: Operations should define a 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-error-400:\n    description: Operations with request bodies should define a 400 Bad Request response\n    severity: warn\n    given: $.paths[*][post,put,patch].responses\n    then:\n      field: '400'\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n  # SCHEMAS — PROPERTY NAMING\n  # ============================================================\n  schema-description:\n    description: Top-level schemas should have a\
  \ description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-type-defined:\n    description: Schema properties should have a type defined\n    severity: warn\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-property-camelCase:\n    description: Schema property names should use camelCase\n    severity: info\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ============================================================\n  # SECURITY\n  # ============================================================\n  security-schemes-defined:\n    description: Security schemes should be defined in components\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  security-global-defined:\n    description: Global\
  \ security should be defined at the spec level\n    severity: warn\n    given: $.security\n    then:\n      function: truthy\n\n  # ============================================================\n  # HTTP METHOD CONVENTIONS\n  # ============================================================\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # ============================================================\n  # GENERAL QUALITY\n  # ============================================================\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: error\n    given: $..description\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \".+\"\n\n  external-docs-encouraged:\n    description: API spec should include externalDocs pointing to documentation\n    severity: info\n    given: $.externalDocs\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/rules/uipath-spectral-rules.yml
tags:
- Automation
- Robotic Process Automation
- RPA
- Artificial Intelligence
- Document Processing
- Enterprise Automation
- Orchestration
- Testing
- Spectral
- Linting
- API Governance
---
