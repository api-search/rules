---
api_specs:
- filename: yugabytedb-aeon-openapi.yml
  format: yaml
  label: YugabyteDB Aeon REST API
  slug: aeon
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/yugabytedb/refs/heads/main/openapi/yugabytedb-aeon-openapi.yml
- filename: yugabytedb-anywhere-v1-universes.yaml
  format: yaml
  label: YugabyteDB Anywhere REST API
  slug: anywhere
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/yugabytedb/refs/heads/main/openapi/yugabytedb-anywhere-v1-universes.yaml
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
- paths
- post
- put
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for YugabyteDB.
layout: rules
name: YugabyteDB API Rules
provider_name: YugabyteDB
provider_slug: yugabytedb
rule_count: 67
rules:
- description: API title should follow the "YugabyteDB ..." naming pattern (e.g. "YugabyteDB Aeon REST API", "YugabyteDB Anywhere v1 — ...")
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
- description: API version should follow the "v{N}" pattern (e.g. v1, v2)
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
- description: Contact should include a documentation or support URL
  given: $.info.contact
  name: info-contact-url
  severity: warn
- description: API info should include license information
  given: $.info
  name: info-license-required
  severity: info
- description: APIs must use OpenAPI 3.0.x or 3.1.x
  given: $.openapi
  name: openapi-version
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-defined
  severity: error
- description: Public-facing server URLs should use HTTPS (variables and relative paths allowed for self-hosted Anywhere)
  given: $.servers[?(@.url && @.url.match(/^https?:\/\//))].url
  name: servers-https-preferred
  severity: warn
- description: Servers should have descriptions
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments should use kebab-case (YugabyteDB Aeon convention; preferred for new endpoints)
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Paths must not contain query strings
  given: $.paths[*]~
  name: paths-no-query-string
  severity: error
- description: Path segments should not use snake_case (prefer kebab-case)
  given: $.paths[*]~
  name: paths-no-snake-case
  severity: warn
- description: Path segments should not use camelCase (prefer kebab-case)
  given: $.paths[*]~
  name: paths-no-camel-case-segment
  severity: info
- description: Anywhere v1 paths use /api/v1/ prefix; Aeon paths do not — both are acceptable for this provider
  given: $.paths[*]~
  name: paths-version-prefix-allowed
  severity: info
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "YugabyteDB Aeon" or "YugabyteDB Anywhere"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-yugabytedb-prefix
  severity: info
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase (e.g. listClusters, createCluster, deleteAllowList)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: operationId should start with a recognized verb (list, get, create, update, delete, restore, pause, resume, attach, detach, upgrade, rollback, restart, finalize, snooze, acknowledge, hide, fetch, run, set, validate, test, precheck, configure)
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
- description: Tags should use Title Case or PascalCase (e.g. "Backup and Restore", "Telemetry Provider", "Clusters", "AllowLists")
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: All global tags should have descriptions
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: All parameters should have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must define a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Parameter names should use snake_case (Aeon convention) or camelCase identifiers like cUUID/uniUUID (Anywhere convention)
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-snake-case
  severity: warn
- description: API keys must be passed in headers, never as query parameters
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-no-api-key-in-query
  severity: error
- description: Use "limit" (not "size", "count", or "perPage") for pagination size
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-limit
  severity: info
- description: Use "offset" or "page" (consistently within an API) for pagination position
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name
  name: parameter-pagination-offset
  severity: info
- description: UUID path parameters should declare format "uuid"
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name.match(/UUID|Uuid|_uuid$|^uuid$|Id$|^id$/))].schema
  name: parameter-uuid-format
  severity: info
- description: Request bodies must support application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: error
- description: Request body schemas should reference a named component (not be inlined)
  given: $.paths[*][post,put,patch].requestBody.content.application/json.schema
  name: request-body-schema-ref
  severity: info
- description: All operations must define at least one response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-defined
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: All operations should define at least one 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: warn
- description: All authenticated operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: GET/PUT/DELETE on resource paths should define a 404 Not Found response
  given: $.paths[?(@property.match(/\{[a-zA-Z]+\}$/))][get,put,delete].responses
  name: response-404-required-for-resource-paths
  severity: warn
- description: POST/PUT/PATCH operations should define a 400 Bad Request response
  given: $.paths[*][post,put,patch].responses
  name: response-400-for-mutations
  severity: info
- description: Operations should document a 500 Server Error response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-500-encouraged
  severity: info
- description: 2xx responses with content should use application/json
  given: $.paths[*][get,post,put,patch,delete].responses[?(@property.match(/^2[0-9]{2}$/))].content
  name: response-success-json-content
  severity: warn
- description: Error response schema should include a message or error field
  given: $.components.schemas.ErrorResponse.properties
  name: response-error-schema-shape
  severity: info
- description: Schema property names should use snake_case (YugabyteDB Aeon convention; preferred for new schemas)
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: warn
- description: Top-level schemas should define a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Top-level schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Identifier properties should be named "id" or end with "_id" (e.g., account_id, cluster_id, project_id)
  given: $.components.schemas[*].properties[?(@property.match(/^[a-zA-Z]*[Ii]dentifier$/))]~
  name: schema-id-property-naming
  severity: info
- description: Timestamp properties should follow the created_at/updated_at convention (Aeon) — avoid creation_date, modified_on
  given: $.components.schemas[*].properties[?(@property.match(/^(creation|modification|deletion)_(date|time|on)$/i))]~
  name: schema-timestamp-naming
  severity: info
- description: Global security requirements should be defined
  given: $
  name: security-global-defined
  severity: warn
- description: Security schemes must be defined under components
  given: $
  name: security-schemes-defined
  severity: error
- description: YugabyteDB APIs should use Bearer auth (Aeon) or API key in the X-AUTH-YW-API-TOKEN header (Anywhere)
  given: $.components.securitySchemes[*]
  name: security-bearer-or-apikey
  severity: warn
- description: Anywhere API key schemes should use the X-AUTH-YW-API-TOKEN header
  given: $.components.securitySchemes[?(@.type == 'apiKey' && @.in == 'header')]
  name: security-apikey-header-name
  severity: info
- description: Security schemes should have a description
  given: $.components.securitySchemes[*]
  name: security-scheme-description
  severity: info
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
- description: APIs should link to external documentation (e.g. docs.yugabyte.com)
  given: $
  name: external-docs-encouraged
  severity: info
rules_file: rules/yugabytedb-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/yugabytedb/refs/heads/main/rules/yugabytedb-spectral-rules.yml
severity_counts:
  error: 17
  hint: 0
  info: 20
  warn: 30
slug: yugabytedb-spectral-rules
source_filename: yugabytedb-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # =====================================================================\n  # INFO / METADATA\n  # =====================================================================\n  info-title-format:\n    description: API title should follow the \"YugabyteDB ...\" naming pattern (e.g. \"YugabyteDB Aeon REST API\", \"YugabyteDB Anywhere v1 — ...\")\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^YugabyteDB .+$\"\n\n  info-description-required:\n    description: API info must have a description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-description-min-length:\n    description: API description should be at least 50 characters\n    severity: warn\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API info must specify a version\n   \
  \ severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-version-format:\n    description: API version should follow the \"v{N}\" pattern (e.g. v1, v2)\n    severity: warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+$\"\n\n  info-contact-required:\n    description: API info should include contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-contact-name:\n    description: Contact should include a name\n    severity: warn\n    given: $.info.contact\n    then:\n      field: name\n      function: truthy\n\n  info-contact-url:\n    description: Contact should include a documentation or support URL\n    severity: warn\n    given: $.info.contact\n    then:\n      field: url\n      function: truthy\n\n  info-license-required:\n    description: API info should include license information\n    severity: info\n\
  \    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  # =====================================================================\n  # OPENAPI VERSION\n  # =====================================================================\n  openapi-version:\n    description: APIs must use OpenAPI 3.0.x or 3.1.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.[01]\\\\.\"\n\n  # =====================================================================\n  # SERVERS\n  # =====================================================================\n  servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-preferred:\n    description: Public-facing server URLs should use HTTPS (variables and relative paths allowed for self-hosted Anywhere)\n    severity: warn\n    given: $.servers[?(@.url\
  \ && @.url.match(/^https?:\\/\\//))].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: Servers should have descriptions\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n  # PATHS — NAMING CONVENTIONS\n  # =====================================================================\n  paths-kebab-case:\n    description: Path segments should use kebab-case (YugabyteDB Aeon convention; preferred for new endpoints)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/([a-z0-9]+(-[a-z0-9]+)*|\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\}))+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n\
  \        notMatch: \"/.+/$\"\n\n  paths-no-query-string:\n    description: Paths must not contain query strings\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  paths-no-snake-case:\n    description: Path segments should not use snake_case (prefer kebab-case)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_\"\n\n  paths-no-camel-case-segment:\n    description: Path segments should not use camelCase (prefer kebab-case)\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/[a-z]+[A-Z][a-zA-Z]*\"\n\n  paths-version-prefix-allowed:\n    description: Anywhere v1 paths use /api/v1/ prefix; Aeon paths do not — both are acceptable for this provider\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n     \
  \   match: \"^(/api/v[0-9]+)?(/[^/]+)+$\"\n\n  # =====================================================================\n  # OPERATIONS\n  # =====================================================================\n  operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-yugabytedb-prefix:\n    description: Operation summaries should start with \"YugabyteDB Aeon\" or \"YugabyteDB Anywhere\"\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^YugabyteDB (Aeon|Anywhere) .+$\"\n\n  operation-description-required:\n    description: All operations should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n\
  \    description: All operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: operationId should use camelCase (e.g. listClusters, createCluster, deleteAllowList)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-id-verb-prefix:\n    description: operationId should start with a recognized verb (list, get, create, update, delete, restore, pause, resume, attach, detach, upgrade, rollback, restart, finalize, snooze, acknowledge, hide, fetch, run, set, validate, test, precheck, configure)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get|create|update|delete|restore|pause|resume|attach|detach|upgrade|rollback|restart|finalize|snooze|acknowledge|hide|fetch|run|set|validate|test|precheck|configure|add|remove|map|unmap|invite|enable|disable|reset|rotate|trigger|cancel|approve|deny|export|import|download|upload|register|deregister|stop|start)[A-Z][a-zA-Z0-9]*$\"\
  \n\n  operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  operation-single-tag:\n    description: Operations should have exactly one tag for clean grouping\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].tags\n    then:\n      function: length\n      functionOptions:\n        max: 1\n\n  # =====================================================================\n  # TAGS\n  # =====================================================================\n  tags-defined-globally:\n    description: Global tags array should be defined at the root\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tags-title-case:\n    description: Tags should use Title Case or PascalCase (e.g. \"Backup and Restore\", \"Telemetry Provider\", \"Clusters\", \"AllowLists\")\n    severity: warn\n  \
  \  given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*((\\\\s(of|to|for|and|the|in|on|a|an)|\\\\s[A-Z0-9][A-Za-z0-9]*))*$\"\n\n  tags-description-required:\n    description: All global tags should have descriptions\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n  # PARAMETERS\n  # =====================================================================\n  parameter-description-required:\n    description: All parameters should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: All parameters must define a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n    \
  \  function: truthy\n\n  parameter-snake-case:\n    description: Parameter names should use snake_case (Aeon convention) or camelCase identifiers like cUUID/uniUUID (Anywhere convention)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9_]*$\"\n\n  parameter-no-api-key-in-query:\n    description: API keys must be passed in headers, never as query parameters\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"(?i)^(api[_-]?key|access[_-]?token|auth[_-]?token|secret)$\"\n\n  parameter-pagination-limit:\n    description: Use \"limit\" (not \"size\", \"count\", or \"perPage\") for pagination size\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n\
  \      function: pattern\n      functionOptions:\n        notMatch: \"^(size|count|perPage|pageSize|page_size|per_page)$\"\n\n  parameter-pagination-offset:\n    description: Use \"offset\" or \"page\" (consistently within an API) for pagination position\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(skip|from|start|startAt|start_at)$\"\n\n  parameter-uuid-format:\n    description: UUID path parameters should declare format \"uuid\"\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path' && @.name.match(/UUID|Uuid|_uuid$|^uuid$|Id$|^id$/))].schema\n    then:\n      field: format\n      function: truthy\n\n  # =====================================================================\n  # REQUEST BODIES\n  # =====================================================================\n  request-body-json-content:\n  \
  \  description: Request bodies must support application/json\n    severity: error\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-schema-ref:\n    description: Request body schemas should reference a named component (not be inlined)\n    severity: info\n    given: $.paths[*][post,put,patch].requestBody.content.application/json.schema\n    then:\n      field: $ref\n      function: truthy\n\n  # =====================================================================\n  # RESPONSES\n  # =====================================================================\n  response-defined:\n    description: All operations must define at least one response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-description-required:\n    description:\
  \ All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-success-required:\n    description: All operations should define at least one 2xx success response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2[0-9]{2}$\": {}\n          minProperties: 1\n\n  response-401-required:\n    description: All authenticated operations should define a 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  response-404-required-for-resource-paths:\n    description: GET/PUT/DELETE on resource paths should define a 404 Not Found response\n    severity: warn\n    given: \"$.paths[?(@property.match(/\\\
  \\{[a-zA-Z]+\\\\}$/))][get,put,delete].responses\"\n    then:\n      field: '404'\n      function: truthy\n\n  response-400-for-mutations:\n    description: POST/PUT/PATCH operations should define a 400 Bad Request response\n    severity: info\n    given: $.paths[*][post,put,patch].responses\n    then:\n      field: '400'\n      function: truthy\n\n  response-500-encouraged:\n    description: Operations should document a 500 Server Error response\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '500'\n      function: truthy\n\n  response-success-json-content:\n    description: 2xx responses with content should use application/json\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[?(@property.match(/^2[0-9]{2}$/))].content\"\n    then:\n      field: application/json\n      function: truthy\n\n  response-error-schema-shape:\n    description: Error response schema should include a message or error field\n\
  \    severity: info\n    given: $.components.schemas.ErrorResponse.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [message]\n            - required: [error]\n\n  # =====================================================================\n  # SCHEMAS — PROPERTY NAMING\n  # =====================================================================\n  schema-property-snake-case:\n    description: Schema property names should use snake_case (YugabyteDB Aeon convention; preferred for new schemas)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  schema-type-defined:\n    description: Top-level schemas should define a type\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  schema-description-required:\n    description:\
  \ Top-level schemas should have a description\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-id-property-naming:\n    description: Identifier properties should be named \"id\" or end with \"_id\" (e.g., account_id, cluster_id, project_id)\n    severity: info\n    given: $.components.schemas[*].properties[?(@property.match(/^[a-zA-Z]*[Ii]dentifier$/))]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*\"\n\n  schema-timestamp-naming:\n    description: Timestamp properties should follow the created_at/updated_at convention (Aeon) — avoid creation_date, modified_on\n    severity: info\n    given: $.components.schemas[*].properties[?(@property.match(/^(creation|modification|deletion)_(date|time|on)$/i))]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*\"\n\n  # =====================================================================\n  # SECURITY\n\
  \  # =====================================================================\n  security-global-defined:\n    description: Global security requirements should be defined\n    severity: warn\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  security-schemes-defined:\n    description: Security schemes must be defined under components\n    severity: error\n    given: $\n    then:\n      field: components.securitySchemes\n      function: truthy\n\n  security-bearer-or-apikey:\n    description: YugabyteDB APIs should use Bearer auth (Aeon) or API key in the X-AUTH-YW-API-TOKEN header (Anywhere)\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          oneOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  const: bearer\n              required: [type, scheme]\n            - properties:\n\
  \                type:\n                  const: apiKey\n                in:\n                  const: header\n              required: [type, in]\n\n  security-apikey-header-name:\n    description: Anywhere API key schemes should use the X-AUTH-YW-API-TOKEN header\n    severity: info\n    given: $.components.securitySchemes[?(@.type == 'apiKey' && @.in == 'header')]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^X-AUTH-YW-API-TOKEN$\"\n\n  security-scheme-description:\n    description: Security schemes should have a description\n    severity: info\n    given: $.components.securitySchemes[*]\n    then:\n      field: description\n      function: truthy\n\n  # =====================================================================\n  # HTTP METHOD CONVENTIONS\n  # =====================================================================\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n\
  \    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  post-has-request-body:\n    description: POST operations should have a request body\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  put-has-request-body:\n    description: PUT operations should have a request body\n    severity: warn\n    given: $.paths[*].put\n    then:\n      field: requestBody\n      function: truthy\n\n  # =====================================================================\n  # GENERAL QUALITY\n  # =====================================================================\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: error\n    given: $..description\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-have-examples:\n    description: Schema properties should include examples\n    severity: info\n    given: \"$.components.schemas[*].properties[?(@.type && @.type != 'object' && @.type != 'array')]\"\n    then:\n      field: example\n      function: truthy\n\n  deprecation-documented:\n    description: Deprecated operations should explain the deprecation in the description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete][?(@.deprecated == true)]\"\n    then:\n      field: description\n      function: truthy\n\n  external-docs-encouraged:\n    description: APIs should link to external documentation (e.g. docs.yugabyte.com)\n    severity: info\n\
  \    given: $\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/yugabytedb/refs/heads/main/rules/yugabytedb-spectral-rules.yml
tags:
- Cloud Database
- Database
- DBaaS
- Distributed SQL
- PostgreSQL
- Spectral
- Linting
- API Governance
---
