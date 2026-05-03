---
api_specs:
- filename: workday-tracking-system-time-tracking-openapi.yml
  format: yaml
  label: Workday Time Tracking API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-tracking-system/refs/heads/main/openapi/workday-tracking-system-time-tracking-openapi.yml
- filename: workday-tracking-system-absence-management-openapi.yml
  format: yaml
  label: Workday Absence Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-tracking-system/refs/heads/main/openapi/workday-tracking-system-absence-management-openapi.yml
- filename: workday-tracking-system-scheduling-openapi.yml
  format: yaml
  label: Workday Scheduling API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-tracking-system/refs/heads/main/openapi/workday-tracking-system-scheduling-openapi.yml
categories:
- delete
- deprecation
- external
- get
- info
- 'no'
- openapi
- operation
- parameter
- patch
- paths
- post
- put
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Workday Tracking System.
layout: rules
name: Workday Tracking System API Rules
provider_name: Workday Tracking System
provider_slug: workday-tracking-system
rule_count: 68
rules:
- description: API title should follow the "Workday ..." naming pattern
  given: $.info.title
  name: info-title-format
  severity: warn
- description: API info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: API description should be at least 50 characters
  given: $.info.description
  name: info-description-min-length
  severity: warn
- description: API info must specify a version
  given: $.info
  name: info-version-required
  severity: error
- description: API version should follow the "v{N}" pattern (e.g. v1)
  given: $.info.version
  name: info-version-format
  severity: warn
- description: API info should include contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Contact should include a name
  given: $.info.contact
  name: info-contact-name
  severity: warn
- description: Contact should include a developer URL
  given: $.info.contact
  name: info-contact-url
  severity: warn
- description: APIs must use OpenAPI 3.0.x
  given: $.openapi
  name: openapi-version
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Server URLs should follow the Workday tenant pattern (e.g. https://{tenant}.workday.com/api/{domain}/v{N})
  given: $.servers[*].url
  name: servers-tenant-pattern
  severity: warn
- description: Servers should have descriptions
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments should use camelCase (Workday convention)
  given: $.paths[*]~
  name: paths-camel-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Paths must not contain query strings
  given: $.paths[*]~
  name: paths-no-query-string
  severity: error
- description: API version belongs in the server URL, not in the path
  given: $.paths[*]~
  name: paths-no-version-prefix
  severity: warn
- description: Worker-specific resources should be scoped under /workers/{workerId}
  given: $.paths[*]~
  name: paths-worker-scoped-when-applicable
  severity: info
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should use Title Case (e.g., "List Time Blocks")
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: operationId should start with a recognized verb (list, get, create, update, delete, request, submit, assign, import, override)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-verb-prefix
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Operations should have exactly one tag for clean grouping
  given: $.paths[*][get,post,put,patch,delete].tags
  name: operation-single-tag
  severity: info
- description: Global tags array should be defined at the root
  given: $
  name: tags-defined-globally
  severity: warn
- description: Tags should use Title Case (e.g. "Time Blocks", "Leave of Absence")
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: All global tags should have descriptions
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: error
- description: Parameter names should use camelCase (Workday convention)
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameter-camel-case
  severity: warn
- description: All parameters must define a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Use "offset" (not "skip", "from", or "page") for pagination offset
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-offset
  severity: warn
- description: Use "limit" (not "size", "count", or "perPage") for pagination size
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-limit
  severity: warn
- description: Date range filters should use startDate/endDate (Workday convention)
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-date-range-naming
  severity: info
- description: Worker identifier path parameter should be named "workerId"
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name =~ /worker/i)].name
  name: parameter-worker-id-naming
  severity: warn
- description: Request bodies should have descriptions
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: Request bodies must support application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: error
- description: Request body schemas should reference a named component (not be inlined)
  given: $.paths[*][post,put,patch].requestBody.content.application/json.schema
  name: request-body-schema-ref
  severity: warn
- description: All operations must define at least one response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: All operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: GET/PUT/DELETE on resource paths should define a 404 Not Found response
  given: $.paths[?(@property.match(/\\{[a-zA-Z]+\\}$/))][get,put,delete].responses
  name: response-404-required-for-resource-paths
  severity: warn
- description: POST/PUT/PATCH operations should define a 400 Bad Request response
  given: $.paths[*][post,put,patch].responses
  name: response-400-for-mutations
  severity: warn
- description: 2xx responses with content should use application/json
  given: $.paths[*][get,post,put,patch,delete].responses[?(@property.match(/^2[0-9]{2}$/))].content
  name: response-success-json-content
  severity: warn
- description: Error responses should reference an error schema with message and error fields
  given: $.components.schemas.ErrorResponse.properties
  name: response-error-schema
  severity: info
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: response-delete-204
  severity: info
- description: Schema property names should use camelCase (Workday convention)
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camel-case
  severity: warn
- description: Top-level schemas must define a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Identifier properties should be named "id" or end with "Id" (e.g., workerId, timeBlockId)
  given: $.components.schemas[*].properties[?(@property.match(/^[a-zA-Z]*[Ii]dentifier$/))]~
  name: schema-id-property-naming
  severity: info
- description: Timestamp properties should follow the createdAt/modifiedAt convention
  given: $.components.schemas[*].properties[?(@property.match(/^(created|modified|updated)[_-]?(date|time|on)$/i))]~
  name: schema-timestamp-naming
  severity: info
- description: Required fields should be declared in a "required" array, not on individual properties
  given: $.components.schemas[*].properties[*]
  name: schema-required-array
  severity: info
- description: Global security requirements should be defined
  given: $
  name: security-global-defined
  severity: warn
- description: Security schemes must be defined under components
  given: $
  name: security-schemes-defined
  severity: error
- description: Workday APIs should expose a BearerAuth scheme using Bearer/JWT
  given: $.components.securitySchemes.BearerAuth
  name: security-bearer-scheme
  severity: warn
- description: Bearer security schemes should declare bearerFormat (e.g. JWT)
  given: $.components.securitySchemes[?(@.scheme == 'bearer')]
  name: security-bearer-format
  severity: warn
- description: Security schemes should have a description
  given: $.components.securitySchemes[*]
  name: security-scheme-description
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: POST operations should have a request body
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: PUT operations should have a request body
  given: $.paths[*].put
  name: put-has-request-body
  severity: warn
- description: PATCH operations should have a request body
  given: $.paths[*].patch
  name: patch-has-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-have-descriptions
  severity: info
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[?(@.type && @.type != 'object' && @.type != 'array')]
  name: schema-properties-have-examples
  severity: info
- description: Deprecated operations should explain the deprecation in the description
  given: $.paths[*][get,post,put,patch,delete][?(@.deprecated == true)]
  name: deprecation-documented
  severity: warn
- description: APIs should link to external documentation
  given: $
  name: external-docs-encouraged
  severity: info
rules_file: rules/workday-tracking-system-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-tracking-system/refs/heads/main/rules/workday-tracking-system-spectral-rules.yml
severity_counts:
  error: 18
  hint: 0
  info: 11
  warn: 39
slug: workday-tracking-system-spectral-rules
source_filename: workday-tracking-system-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # =====================================================================\n  # INFO / METADATA\n  # =====================================================================\n  info-title-format:\n    description: API title should follow the \"Workday ...\" naming pattern\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday .+ API$\"\n\n  info-description-required:\n    description: API info must have a description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-description-min-length:\n    description: API description should be at least 50 characters\n    severity: warn\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API info must specify a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n  \
  \    function: truthy\n\n  info-version-format:\n    description: API version should follow the \"v{N}\" pattern (e.g. v1)\n    severity: warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+$\"\n\n  info-contact-required:\n    description: API info should include contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-contact-name:\n    description: Contact should include a name\n    severity: warn\n    given: $.info.contact\n    then:\n      field: name\n      function: truthy\n\n  info-contact-url:\n    description: Contact should include a developer URL\n    severity: warn\n    given: $.info.contact\n    then:\n      field: url\n      function: truthy\n\n  # =====================================================================\n  # OPENAPI VERSION\n  # =====================================================================\n  openapi-version:\n    description:\
  \ APIs must use OpenAPI 3.0.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # =====================================================================\n  # SERVERS\n  # =====================================================================\n  servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-tenant-pattern:\n    description: Server URLs should follow the Workday tenant pattern (e.g. https://{tenant}.workday.com/api/{domain}/v{N})\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\\\
  \\{tenant\\\\}\\\\.workday\\\\.com/api/[a-z][a-z-]*/v[0-9]+$\"\n\n  servers-description-required:\n    description: Servers should have descriptions\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n  # PATHS — NAMING CONVENTIONS\n  # =====================================================================\n  paths-camel-case:\n    description: Path segments should use camelCase (Workday convention)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/([a-z][a-zA-Z0-9]*|\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\}))+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-no-query-string:\n    description: Paths must not contain\
  \ query strings\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  paths-no-version-prefix:\n    description: API version belongs in the server URL, not in the path\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/v[0-9]+(/|$)\"\n\n  paths-worker-scoped-when-applicable:\n    description: Worker-specific resources should be scoped under /workers/{workerId}\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/(timeBlocks|timeOff|timeRequests|timesheets|timeClockEvents|workSchedule|leaveOfAbsence|balances|accruals)(/|$)\"\n\n  # =====================================================================\n  # OPERATIONS\n  # =====================================================================\n  operation-summary-required:\n    description: All operations must\
  \ have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries should use Title Case (e.g., \"List Time Blocks\")\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*(\\\\s[A-Z0-9][A-Za-z0-9-]*)*$\"\n\n  operation-description-required:\n    description: All operations should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: operationId should use camelCase\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-id-verb-prefix:\n    description: operationId should start with a recognized verb (list, get, create, update, delete, request, submit, assign, import, override)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get|create|update|delete|request|submit|assign|import|override|cancel|approve|deny|return)[A-Z][a-zA-Z0-9]+$\"\n\n  operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-single-tag:\n    description: Operations should have exactly one tag for clean grouping\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].tags\n\
  \    then:\n      function: length\n      functionOptions:\n        max: 1\n\n  # =====================================================================\n  # TAGS\n  # =====================================================================\n  tags-defined-globally:\n    description: Global tags array should be defined at the root\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tags-title-case:\n    description: Tags should use Title Case (e.g. \"Time Blocks\", \"Leave of Absence\")\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s(of|to|for|and|the|in|on)|\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  tags-description-required:\n    description: All global tags should have descriptions\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n \
  \ # PARAMETERS\n  # =====================================================================\n  parameter-description-required:\n    description: All parameters must have descriptions\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-camel-case:\n    description: Parameter names should use camelCase (Workday convention)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  parameter-schema-required:\n    description: All parameters must define a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  parameter-pagination-offset:\n    description: Use \"offset\" (not \"skip\", \"from\", or \"page\") for pagination offset\n    severity: warn\n    given:\
  \ $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(skip|from|page|pageNumber|pageNum)$\"\n\n  parameter-pagination-limit:\n    description: Use \"limit\" (not \"size\", \"count\", or \"perPage\") for pagination size\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(size|count|perPage|pageSize)$\"\n\n  parameter-date-range-naming:\n    description: Date range filters should use startDate/endDate (Workday convention)\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(fromDate|toDate|dateFrom|dateTo|begin|end)$\"\n\n  parameter-worker-id-naming:\n    description: Worker identifier path parameter should be named\
  \ \"workerId\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name =~ /worker/i)].name\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - workerId\n\n  # =====================================================================\n  # REQUEST BODIES\n  # =====================================================================\n  request-body-description:\n    description: Request bodies should have descriptions\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  request-body-json-content:\n    description: Request bodies must support application/json\n    severity: error\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-schema-ref:\n    description: Request body schemas should reference a named component (not be inlined)\n\
  \    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content.application/json.schema\n    then:\n      field: $ref\n      function: truthy\n\n  # =====================================================================\n  # RESPONSES\n  # =====================================================================\n  response-success-required:\n    description: All operations must define at least one response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-description-required:\n    description: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-required:\n    description: All operations should define a 401 Unauthorized response\n    severity: warn\n    given:\
  \ $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-404-required-for-resource-paths:\n    description: GET/PUT/DELETE on resource paths should define a 404 Not Found response\n    severity: warn\n    given: $.paths[?(@property.match(/\\\\{[a-zA-Z]+\\\\}$/))][get,put,delete].responses\n    then:\n      field: '404'\n      function: truthy\n\n  response-400-for-mutations:\n    description: POST/PUT/PATCH operations should define a 400 Bad Request response\n    severity: warn\n    given: $.paths[*][post,put,patch].responses\n    then:\n      field: '400'\n      function: truthy\n\n  response-success-json-content:\n    description: 2xx responses with content should use application/json\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[?(@property.match(/^2[0-9]{2}$/))].content\n    then:\n      field: application/json\n      function: truthy\n\n  response-error-schema:\n    description: Error responses\
  \ should reference an error schema with message and error fields\n    severity: info\n    given: $.components.schemas.ErrorResponse.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - error\n            - message\n\n  response-delete-204:\n    description: DELETE operations should return 204 No Content\n    severity: info\n    given: $.paths[*].delete.responses\n    then:\n      field: '204'\n      function: truthy\n\n  # =====================================================================\n  # SCHEMAS — PROPERTY NAMING\n  # =====================================================================\n  schema-property-camel-case:\n    description: Schema property names should use camelCase (Workday convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-type-defined:\n\
  \    description: Top-level schemas must define a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-description-required:\n    description: Top-level schemas should have a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-id-property-naming:\n    description: Identifier properties should be named \"id\" or end with \"Id\" (e.g., workerId, timeBlockId)\n    severity: info\n    given: $.components.schemas[*].properties[?(@property.match(/^[a-zA-Z]*[Ii]dentifier$/))]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*\"\n\n  schema-timestamp-naming:\n    description: Timestamp properties should follow the createdAt/modifiedAt convention\n    severity: info\n    given: $.components.schemas[*].properties[?(@property.match(/^(created|modified|updated)[_-]?(date|time|on)$/i))]~\n    then:\n    \
  \  function: pattern\n      functionOptions:\n        notMatch: \".*\"\n\n  schema-required-array:\n    description: Required fields should be declared in a \"required\" array, not on individual properties\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: required\n      function: falsy\n\n  # =====================================================================\n  # SECURITY\n  # =====================================================================\n  security-global-defined:\n    description: Global security requirements should be defined\n    severity: warn\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  security-schemes-defined:\n    description: Security schemes must be defined under components\n    severity: error\n    given: $\n    then:\n      field: components.securitySchemes\n      function: truthy\n\n  security-bearer-scheme:\n    description: Workday APIs should expose a BearerAuth scheme using Bearer/JWT\n\
  \    severity: warn\n    given: $.components.securitySchemes.BearerAuth\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - type\n            - scheme\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  security-bearer-format:\n    description: Bearer security schemes should declare bearerFormat (e.g. JWT)\n    severity: warn\n    given: $.components.securitySchemes[?(@.scheme == 'bearer')]\n    then:\n      field: bearerFormat\n      function: truthy\n\n  security-scheme-description:\n    description: Security schemes should have a description\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n  # HTTP METHOD CONVENTIONS\n  # =====================================================================\n\
  \  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  post-has-request-body:\n    description: POST operations should have a request body\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  put-has-request-body:\n    description: PUT operations should have a request body\n    severity: warn\n    given: $.paths[*].put\n    then:\n      field: requestBody\n      function: truthy\n\n  patch-has-request-body:\n    description: PATCH operations should have a request body\n    severity: warn\n    given: $.paths[*].patch\n    then:\n      field: requestBody\n      function: truthy\n\n  #\
  \ =====================================================================\n  # GENERAL QUALITY\n  # =====================================================================\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: error\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-have-examples:\n    description: Schema properties should include examples\n    severity: info\n    given: $.components.schemas[*].properties[?(@.type && @.type != 'object' && @.type != 'array')]\n    then:\n      field: example\n      function: truthy\n\n  deprecation-documented:\n    description: Deprecated operations should explain the deprecation in the description\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,patch,delete][?(@.deprecated == true)]\n    then:\n      field: description\n      function: truthy\n\n  external-docs-encouraged:\n    description: APIs should link to external documentation\n    severity: info\n    given: $\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-tracking-system/refs/heads/main/rules/workday-tracking-system-spectral-rules.yml
tags:
- Absence Management
- Attendance
- Enterprise
- HCM
- Human Capital Management
- Payroll
- Scheduling
- Time Tracking
- Timesheets
- Workforce Management
- Spectral
- Linting
- API Governance
---
