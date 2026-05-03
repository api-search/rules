---
api_specs:
- filename: Recruiting_OpenAPI.yaml
  format: yaml
  label: Workday Recruiting REST API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Recruiting/v41.2/Recruiting_OpenAPI.yaml
categories:
- collection
- delete
- deprecation
- examples
- external
- get
- global
- info
- 'no'
- openapi
- operation
- parameter
- patch
- paths
- post
- put
- reference
- request
- resource
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Workday Recruiting.
layout: rules
name: Workday Recruiting API Rules
provider_name: Workday Recruiting
provider_slug: workday-recruiting
rule_count: 67
rules:
- description: API title must follow the Workday Recruiting naming pattern
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
- description: Version should follow the v{n} or v{n}.{n} pattern (e.g. v1, v41.2)
  given: $.info.version
  name: info-version-format
  severity: warn
- description: API info must include contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: API info should reference Workday terms of service
  given: $.info
  name: info-terms-of-service
  severity: info
- description: APIs should provide external documentation links
  given: $
  name: external-docs-required
  severity: info
- description: APIs must use OpenAPI 3.1.x
  given: $.openapi
  name: openapi-version
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: All servers should include a description
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Server URLs should include a version segment (e.g. /v41.2)
  given: $.servers[*].url
  name: servers-versioned-path
  severity: warn
- description: Server URLs should include the /recruiting/ API segment
  given: $.servers[*].url
  name: servers-recruiting-path
  severity: info
- description: Path segments must use camelCase resource names (Workday convention)
  given: $.paths[*]~
  name: paths-camel-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Paths must not contain query strings
  given: $.paths[*]~
  name: paths-no-query-strings
  severity: error
- description: Top-level collection paths should use plural resource nouns
  given: $.paths[*]~
  name: paths-plural-resources
  severity: info
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Workday Recruiting"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: operationId should start with a recognized recruiting verb
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-verb-prefix
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Top-level tags array should be defined for documentation grouping
  given: $
  name: global-tags-defined
  severity: warn
- description: Global tag names should use Title Case (multi-word allowed)
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: All global tags must have descriptions
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: All parameters must have descriptions
  given: '#Parameter'
  name: parameter-description-required
  severity: error
- description: Parameter names should use camelCase (Workday convention)
  given: '#Parameter'
  name: parameter-camel-case
  severity: warn
- description: All parameters must define a schema
  given: '#Parameter'
  name: parameter-schema-required
  severity: error
- description: Pagination should use a "limit" parameter, not page-size or perPage
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-limit
  severity: warn
- description: Pagination should use an "offset" parameter, not page or pageNumber
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-offset
  severity: warn
- description: API keys must not be passed as query parameters
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-no-api-key-in-query
  severity: error
- description: Resource identifier path parameters should be named "id" (Workday WID convention)
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name =~ /id$/i)].name
  name: resource-id-path-param-naming
  severity: info
- description: Request bodies must support application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: error
- description: Request body content must reference a schema
  given: $.paths[*][post,put,patch].requestBody.content[*]
  name: request-body-schema-required
  severity: warn
- description: All operations must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: GET operations on a single resource should define a 404 Not Found response
  given: $.paths[?(@property.match(/\\{[a-zA-Z]+\\}$/))].get.responses
  name: response-404-on-resource-get
  severity: warn
- description: POST/PUT/PATCH operations should define a 400 Bad Request response
  given: $.paths[*][post,put,patch].responses
  name: response-400-on-mutations
  severity: warn
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Success responses must use application/json content type
  given: $.paths[*][get,post,put,patch,delete].responses['200','201','202'].content
  name: response-json-content
  severity: warn
- description: Reusable error responses should reference a schema with message/error fields
  given: $.components.responses[*].content.application/json
  name: response-error-schema-fields
  severity: warn
- description: Schema property names must use camelCase (Workday convention)
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camel-case
  severity: warn
- description: Top-level schemas must define a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Top-level schemas should include a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Resource id properties must be strings (Workday WID convention)
  given: $.components.schemas[*].properties.id
  name: schema-id-property-string
  severity: warn
- description: createdOn, updatedOn, submittedOn, postedOn, scheduledOn, completedOn properties should use date-time format
  given: $.components.schemas[*].properties[?(@property.match(/^(createdOn|updatedOn|submittedOn|postedOn|scheduledOn|completedOn|approvedOn|processedOn|startedAt|completedAt)$/))]
  name: schema-timestamps-date-time
  severity: warn
- description: targetHireDate, targetEndDate, postingStartDate, postingEndDate, interviewDate, fromDate, toDate properties should use date format
  given: $.components.schemas[*].properties[?(@property.match(/^(targetHireDate|targetEndDate|postingStartDate|postingEndDate|interviewDate|fromDate|toDate|startDate|endDate|effectiveDate)$/))]
  name: schema-recruiting-date-format
  severity: warn
- description: Collection (list) responses must include a data array property
  given: $.paths[*].get.responses['200'].content.application/json.schema.properties
  name: collection-response-data-array
  severity: warn
- description: Collection (list) responses should include a total property indicating full result count
  given: $.paths[*].get.responses['200'].content.application/json.schema.properties
  name: collection-response-total
  severity: warn
- description: Reference schema must have id and descriptor properties (Workday Reference convention)
  given: $.components.schemas.Reference.properties
  name: reference-schema-shape
  severity: warn
- description: Global security must be declared
  given: $
  name: global-security-defined
  severity: error
- description: Security schemes must be defined under components
  given: $
  name: security-schemes-defined
  severity: error
- description: An oauth2 security scheme is required for Workday Recruiting APIs
  given: $.components.securitySchemes
  name: security-oauth2-required
  severity: error
- description: The oauth2 security scheme must declare type oauth2
  given: $.components.securitySchemes.oauth2
  name: security-oauth2-type
  severity: error
- description: The oauth2 security scheme must define flows
  given: $.components.securitySchemes.oauth2
  name: security-oauth2-flows
  severity: error
- description: Security schemes must include a description
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
- description: PATCH operations must have a request body
  given: $.paths[*].patch
  name: patch-has-request-body
  severity: error
- description: PUT operations must have a request body
  given: $.paths[*].put
  name: put-has-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Response and request examples improve developer experience
  given: $.paths[*][get,post,put,patch,delete].responses['200','201'].content.application/json
  name: examples-encouraged
  severity: info
- description: Deprecated operations should explain the migration path in their description
  given: $.paths[*][?(@.deprecated == true)]
  name: deprecation-documented
  severity: warn
rules_file: rules/workday-recruiting-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-recruiting/refs/heads/main/rules/workday-recruiting-spectral-rules.yml
severity_counts:
  error: 25
  hint: 0
  info: 6
  warn: 36
slug: workday-recruiting-spectral-rules
source_filename: workday-recruiting-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-format:\n    description: API title must follow the Workday Recruiting naming pattern\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday Recruiting .+\"\n\n  info-description-required:\n    description: API info must have a description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-description-min-length:\n    description: API description should be at least 50 characters\n    severity: warn\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API info must specify a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-version-format:\n    description: Version should follow the v{n} or v{n}.{n} pattern (e.g. v1, v41.2)\n    severity:\
  \ warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+(\\\\.[0-9]+)?$\"\n\n  info-contact-required:\n    description: API info must include contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-terms-of-service:\n    description: API info should reference Workday terms of service\n    severity: info\n    given: $.info\n    then:\n      field: termsOfService\n      function: truthy\n\n  external-docs-required:\n    description: APIs should provide external documentation links\n    severity: info\n    given: $\n    then:\n      field: externalDocs\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version:\n    description: APIs must use OpenAPI 3.1.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least\
  \ one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: All servers should include a description\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  servers-versioned-path:\n    description: Server URLs should include a version segment (e.g. /v41.2)\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]+(\\\\.[0-9]+)?(/|$)\"\n\n  servers-recruiting-path:\n    description: Server URLs should include the /recruiting/ API segment\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"/recruiting/\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-camel-case:\n    description: Path segments must use camelCase resource names (Workday convention)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-zA-Z0-9]*(/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})?)+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-no-query-strings:\n    description: Paths must not contain query strings\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  paths-plural-resources:\n    description: Top-level collection paths should use plural resource nouns\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^/[a-z][a-zA-Z0-9]*(s|es|ies|Statuses|Sites|Categories|Brands|Regions|Packages|Postings|Settings|Calendars)(/.*)?$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-prefix:\n    description: Operation summaries should start with \"Workday Recruiting\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday Recruiting \"\n\n  operation-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n\
  \    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-id-verb-prefix:\n    description: operationId should start with a recognized recruiting verb\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get|create|update|edit|delete|close|manage|add|assess|refer|move|offer|post|unpost|submit|initiate|import|schedule)[A-Z]\"\n\n  operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  global-tags-defined:\n    description: Top-level tags\
  \ array should be defined for documentation grouping\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tags-title-case:\n    description: Global tag names should use Title Case (multi-word allowed)\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z]*((-|\\\\s)[A-Z][A-Za-z]*)*$\"\n\n  tags-description-required:\n    description: All global tags must have descriptions\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have descriptions\n    severity: error\n    given: \"#Parameter\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-camel-case:\n    description: Parameter names should use camelCase (Workday convention)\n    severity: warn\n    given: \"#Parameter\"\n    then:\n      field: name\n\
  \      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  parameter-schema-required:\n    description: All parameters must define a schema\n    severity: error\n    given: \"#Parameter\"\n    then:\n      field: schema\n      function: truthy\n\n  parameter-pagination-limit:\n    description: Pagination should use a \"limit\" parameter, not page-size or perPage\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(pageSize|perPage|page_size|per_page|size)$\"\n\n  parameter-pagination-offset:\n    description: Pagination should use an \"offset\" parameter, not page or pageNumber\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(page|pageNumber|page_number|pageNo)$\"\n\n  parameter-no-api-key-in-query:\n\
  \    description: API keys must not be passed as query parameters\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"(?i)(api[_-]?key|apikey|access[_-]?token|token)\"\n\n  resource-id-path-param-naming:\n    description: Resource identifier path parameters should be named \"id\" (Workday WID convention)\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name =~ /id$/i)].name\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - id\n\n  # REQUEST BODIES\n  request-body-json-content:\n    description: Request bodies must support application/json content type\n    severity: error\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-schema-required:\n    description: Request body\
  \ content must reference a schema\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content[*]\n    then:\n      field: schema\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: All operations must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2[0-9][0-9]$\": {}\n          minProperties: 1\n\n  response-401-required:\n    description: Operations should define a 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-404-on-resource-get:\n    description: GET operations on a single resource should define a 404 Not Found response\n    severity: warn\n    given: $.paths[?(@property.match(/\\\\{[a-zA-Z]+\\\
  \\}$/))].get.responses\n    then:\n      field: '404'\n      function: truthy\n\n  response-400-on-mutations:\n    description: POST/PUT/PATCH operations should define a 400 Bad Request response\n    severity: warn\n    given: $.paths[*][post,put,patch].responses\n    then:\n      field: '400'\n      function: truthy\n\n  response-description-required:\n    description: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-json-content:\n    description: Success responses must use application/json content type\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses['200','201','202'].content\n    then:\n      field: application/json\n      function: truthy\n\n  response-error-schema-fields:\n    description: Reusable error responses should reference a schema with message/error fields\n    severity: warn\n    given: $.components.responses[*].content.application/json\n\
  \    then:\n      field: schema\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-property-camel-case:\n    description: Schema property names must use camelCase (Workday convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-type-defined:\n    description: Top-level schemas must define a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-description-required:\n    description: Top-level schemas should include a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-id-property-string:\n    description: Resource id properties must be strings (Workday WID convention)\n    severity: warn\n    given: $.components.schemas[*].properties.id\n    then:\n      field: type\n      function:\
  \ enumeration\n      functionOptions:\n        values:\n          - string\n\n  schema-timestamps-date-time:\n    description: createdOn, updatedOn, submittedOn, postedOn, scheduledOn, completedOn properties should use date-time format\n    severity: warn\n    given: $.components.schemas[*].properties[?(@property.match(/^(createdOn|updatedOn|submittedOn|postedOn|scheduledOn|completedOn|approvedOn|processedOn|startedAt|completedAt)$/))]\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  schema-recruiting-date-format:\n    description: targetHireDate, targetEndDate, postingStartDate, postingEndDate, interviewDate, fromDate, toDate properties should use date format\n    severity: warn\n    given: $.components.schemas[*].properties[?(@property.match(/^(targetHireDate|targetEndDate|postingStartDate|postingEndDate|interviewDate|fromDate|toDate|startDate|endDate|effectiveDate)$/))]\n    then:\n      field: format\n\
  \      function: enumeration\n      functionOptions:\n        values:\n          - date\n\n  collection-response-data-array:\n    description: Collection (list) responses must include a data array property\n    severity: warn\n    given: $.paths[*].get.responses['200'].content.application/json.schema.properties\n    then:\n      field: data\n      function: truthy\n\n  collection-response-total:\n    description: Collection (list) responses should include a total property indicating full result count\n    severity: warn\n    given: $.paths[*].get.responses['200'].content.application/json.schema.properties\n    then:\n      field: total\n      function: truthy\n\n  reference-schema-shape:\n    description: Reference schema must have id and descriptor properties (Workday Reference convention)\n    severity: warn\n    given: $.components.schemas.Reference.properties\n    then:\n      field: descriptor\n      function: truthy\n\n  # SECURITY\n  global-security-defined:\n    description: Global\
  \ security must be declared\n    severity: error\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  security-schemes-defined:\n    description: Security schemes must be defined under components\n    severity: error\n    given: $\n    then:\n      field: components.securitySchemes\n      function: truthy\n\n  security-oauth2-required:\n    description: An oauth2 security scheme is required for Workday Recruiting APIs\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      field: oauth2\n      function: truthy\n\n  security-oauth2-type:\n    description: The oauth2 security scheme must declare type oauth2\n    severity: error\n    given: $.components.securitySchemes.oauth2\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - oauth2\n\n  security-oauth2-flows:\n    description: The oauth2 security scheme must define flows\n    severity: error\n    given: $.components.securitySchemes.oauth2\n\
  \    then:\n      field: flows\n      function: truthy\n\n  security-scheme-description:\n    description: Security schemes must include a description\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: description\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  post-has-request-body:\n    description: POST operations should have a request body\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  patch-has-request-body:\n    description: PATCH operations must have a request body\n    severity:\
  \ error\n    given: $.paths[*].patch\n    then:\n      field: requestBody\n      function: truthy\n\n  put-has-request-body:\n    description: PUT operations must have a request body\n    severity: error\n    given: $.paths[*].put\n    then:\n      field: requestBody\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: error\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  examples-encouraged:\n    description: Response and request examples improve developer experience\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].responses['200','201'].content.application/json\n    then:\n      field: examples\n      function: truthy\n\n  deprecation-documented:\n    description: Deprecated operations should explain the migration path in their description\n    severity: warn\n    given: $.paths[*][?(@.deprecated == true)]\n\
  \    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-recruiting/refs/heads/main/rules/workday-recruiting-spectral-rules.yml
tags:
- HCM
- Human Resources
- Recruiting
- SaaS
- Talent Acquisition
- Spectral
- Linting
- API Governance
---
