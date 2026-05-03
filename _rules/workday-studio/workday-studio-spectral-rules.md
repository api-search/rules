---
api_specs:
- filename: workday-studio-integration-openapi.yml
  format: yaml
  label: Workday Studio Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-studio/refs/heads/main/openapi/workday-studio-integration-openapi.yml
- filename: workday-studio-web-services-openapi.yml
  format: yaml
  label: Workday Web Services API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-studio/refs/heads/main/openapi/workday-studio-web-services-openapi.yml
categories:
- deprecation
- examples
- external
- info
- 'no'
- openapi
- operation
- parameter
- paths
- put
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Workday Studio.
layout: rules
name: Workday Studio API Rules
provider_name: Workday Studio
provider_slug: workday-studio
rule_count: 64
rules:
- description: The info object must include a title.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Workday Studio".
  given: $.info.title
  name: info-title-workday-studio-prefix
  severity: warn
- description: The info object must include a description.
  given: $.info
  name: info-description-required
  severity: error
- description: info.description should provide meaningful context (>= 100 chars).
  given: $.info.description
  name: info-description-min-length
  severity: warn
- description: The info object must include a version.
  given: $.info
  name: info-version-required
  severity: error
- description: A contact object should be defined for support.
  given: $.info
  name: info-contact-required
  severity: warn
- description: Contact email should be the Workday API support address.
  given: $.info.contact.email
  name: info-contact-email-workday
  severity: info
- description: A license object should be defined.
  given: $.info
  name: info-license-required
  severity: warn
- description: termsOfService should be set on info.
  given: $.info
  name: info-terms-of-service-recommended
  severity: info
- description: Specs in this repo must declare OpenAPI 3.1.0.
  given: $.openapi
  name: openapi-version-3-1
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Every server must include a description.
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Server URLs should template both baseUrl and tenant variables.
  given: $.servers[*].url
  name: servers-tenant-templated
  severity: warn
- description: Paths may use camelCase (e.g. /integrationSystems) or Workday SOAP-style PascalCase_With_Underscores (e.g. /Human_Resources/Get_Workers). No spaces, hyphens, or other special characters.
  given: $.paths
  name: paths-allowed-character-set
  severity: error
- description: Paths must not end with a trailing slash (except the root).
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: Path templates must not include query strings.
  given: $.paths
  name: paths-no-query-strings
  severity: error
- description: Paths should not include file extensions.
  given: $.paths
  name: paths-no-file-extensions
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should begin with "Workday Studio ".
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-workday-studio-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationId-required
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-operationId-camelcase
  severity: error
- description: operationId should begin with an approved verb prefix (get, list, create, update, delete, launch, search).
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-operationId-verb-prefix
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Operation tags array must not be empty.
  given: $.paths[*][get,post,put,patch,delete,head,options].tags
  name: operation-tag-count
  severity: error
- description: A top-level tags array must be defined.
  given: $
  name: tags-defined-globally
  severity: error
- description: Every tag must have a name.
  given: $.tags[*]
  name: tags-name-required
  severity: error
- description: Every tag must have a description.
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: Tag names should use Title Case (e.g. "Integration Assemblies", "Human Resources", "Benefits Administration").
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: Every tag referenced on an operation must be defined in the global tags array.
  given: $.paths[*][get,post,put,patch,delete,head,options].tags[*]
  name: operation-tags-must-be-defined-globally
  severity: warn
- description: Every parameter must have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameter names should use camelCase. The path identifier "ID" is permitted as the canonical Workday resource identifier.
  given: $..parameters[*].name
  name: parameter-name-camelcase
  severity: warn
- description: API keys must not be passed as query parameters.
  given: $..parameters[?(@.in == 'query')].name
  name: parameter-no-apikey-in-query
  severity: error
- description: Standardize pagination on limit/offset. The web services spec uses pageSize/page; new operations should adopt limit/offset.
  given: $..parameters[?(@.in == 'query')].name
  name: parameter-pagination-uses-limit-offset
  severity: warn
- description: Request bodies must support application/json.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: error
- description: Request bodies should include a description.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description-recommended
  severity: info
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: Operations should declare a 401 response since the API requires authentication.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-401-required
  severity: warn
- description: Operations should declare a 403 response for permission errors.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-403-recommended
  severity: warn
- description: Operations on /{ID} paths should declare a 404 response.
  given: $.paths[?(@property.match(/\{[A-Za-z]+\}/))][get,post,put,patch,delete].responses
  name: response-404-on-id-paths
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[*]
  name: response-description-required
  severity: error
- description: 2xx responses must return application/json.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[?(@property.match(/^2[0-9][0-9]$/))].content
  name: response-2xx-json-content
  severity: warn
- description: The shared ErrorResponse schema should expose a message-bearing field.
  given: $.components.schemas.ErrorResponse.properties
  name: response-error-schema-has-message
  severity: warn
- description: Collection responses should use the standard {total, data[]} wrapper shape used throughout the Workday Studio specs.
  given: $.components.schemas[?(@property.match(/Response$/))].properties
  name: response-list-uses-total-data-wrapper
  severity: warn
- description: Schema property names should use camelCase. The canonical "ID" path identifier is permitted at any depth.
  given: $.components.schemas..properties
  name: schema-property-name-camelcase
  severity: warn
- description: Resource identifier properties should be named "id" (lowercase), matching the convention used across the Workday Studio specs.
  given: $.components.schemas..properties
  name: schema-id-property-name
  severity: warn
- description: Date-time properties should be named with a "DateTime" suffix (e.g. startDateTime, endDateTime, lastRunDateTime).
  given: $.components.schemas..properties[?(@.format == 'date-time')]~
  name: schema-timestamp-property-suffix
  severity: info
- description: Date-only properties should be named with a "Date" suffix (e.g. hireDate, startDate, effectiveDate).
  given: $.components.schemas..properties[?(@.format == 'date')]~
  name: schema-date-property-suffix
  severity: info
- description: Top-level schemas in components should include a description.
  given: $.components.schemas[*]
  name: schema-top-level-description
  severity: info
- description: Every schema definition should declare a type.
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: A global security requirement must be defined.
  given: $
  name: security-global-defined
  severity: error
- description: components.securitySchemes must be defined.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Specs must define an OAuth2 security scheme named "OAuth2".
  given: $.components.securitySchemes
  name: security-oauth2-required
  severity: error
- description: The OAuth2 scheme must declare an authorizationCode flow.
  given: $.components.securitySchemes.OAuth2.flows
  name: security-oauth2-flow-authorization-code
  severity: warn
- description: OAuth2 tokenUrl should template the tenant in the path.
  given: $.components.securitySchemes.OAuth2.flows.authorizationCode.tokenUrl
  name: security-oauth2-token-url-tenant
  severity: info
- description: OAuth2 scope names should use the Workday Studio convention of "<r|w>:<resource>" (e.g. r:integrations, w:integrations, r:wws, w:wws).
  given: $.components.securitySchemes.OAuth2.flows.authorizationCode.scopes
  name: security-scope-naming
  severity: warn
- description: GET operations must not declare a request body.
  given: $.paths[*].get
  name: no-request-body-on-get
  severity: error
- description: DELETE operations should not declare a request body.
  given: $.paths[*].delete
  name: no-request-body-on-delete
  severity: warn
- description: PUT and PATCH operations must declare a request body.
  given: $.paths[*][put,patch]
  name: put-patch-request-body-required
  severity: warn
- description: Description fields, when present, must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: A top-level externalDocs object is encouraged for discoverability.
  given: $
  name: external-docs-encouraged
  severity: info
- description: Adding examples to schemas helps consumers understand payloads.
  given: $.components.schemas[*]
  name: examples-encouraged
  severity: info
- description: Deprecated operations must explain the deprecation in their description.
  given: $.paths[*][get,post,put,patch,delete,head,options][?(@.deprecated == true)].description
  name: deprecation-must-be-documented
  severity: warn
rules_file: rules/workday-studio-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-studio/refs/heads/main/rules/workday-studio-spectral-rules.yml
severity_counts:
  error: 25
  hint: 0
  info: 9
  warn: 30
slug: workday-studio-spectral-rules
source_filename: workday-studio-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# =============================================================================\n# Workday Studio Spectral Ruleset\n# =============================================================================\n# Opinionated rules derived from the Workday Studio OpenAPI specifications:\n#   - openapi/workday-studio-integration-openapi.yml\n#   - openapi/workday-studio-web-services-openapi.yml\n#\n# Run with:\n#   spectral lint -r rules/workday-studio-spectral-rules.yml openapi/*.yml\n# =============================================================================\n\nrules:\n\n  # ===========================================================================\n  # INFO / METADATA\n  # ===========================================================================\n\n  info-title-required:\n    description: The info object must include a title.\n    message: \"info.title is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-workday-studio-prefix:\n\
  \    description: API title should start with \"Workday Studio\".\n    message: 'info.title should begin with \"Workday Studio\" (got \"{{value}}\").'\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday Studio\\\\b\"\n\n  info-description-required:\n    description: The info object must include a description.\n    message: \"info.description is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-description-min-length:\n    description: info.description should provide meaningful context (>= 100 chars).\n    message: \"info.description should be at least 100 characters.\"\n    severity: warn\n    given: \"$.info.description\"\n    then:\n      function: length\n      functionOptions:\n        min: 100\n\n  info-version-required:\n    description: The info object must include a version.\n    message: \"info.version is required.\"\n\
  \    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: A contact object should be defined for support.\n    message: \"info.contact should be defined.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  info-contact-email-workday:\n    description: Contact email should be the Workday API support address.\n    message: \"info.contact.email should be api-support@workday.com.\"\n    severity: info\n    given: \"$.info.contact.email\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^api-support@workday\\\\.com$\"\n\n  info-license-required:\n    description: A license object should be defined.\n    message: \"info.license should be defined.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  info-terms-of-service-recommended:\n    description: termsOfService should\
  \ be set on info.\n    message: \"info.termsOfService should be defined.\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: termsOfService\n      function: truthy\n\n  # ===========================================================================\n  # OPENAPI VERSION\n  # ===========================================================================\n\n  openapi-version-3-1:\n    description: Specs in this repo must declare OpenAPI 3.1.0.\n    message: 'openapi must be \"3.1.0\" (got \"{{value}}\").'\n    severity: error\n    given: \"$.openapi\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.0$\"\n\n  # ===========================================================================\n  # SERVERS\n  # ===========================================================================\n\n  servers-defined:\n    description: At least one server must be defined.\n    message: \"servers must be defined and non-empty.\"\n    severity: error\n  \
  \  given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS.\n    message: 'Server URL \"{{value}}\" must use https://.'\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: Every server must include a description.\n    message: \"Each server should have a description.\"\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: description\n      function: truthy\n\n  servers-tenant-templated:\n    description: Server URLs should template both baseUrl and tenant variables.\n    message: 'Server URL should include {baseUrl} and {tenant} variables (got \"{{value}}\").'\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{baseUrl\\\\}.*\\\\{tenant\\\\}\"\n\n  # ===========================================================================\n\
  \  # PATHS — NAMING CONVENTIONS\n  # ===========================================================================\n\n  paths-allowed-character-set:\n    description: >-\n      Paths may use camelCase (e.g. /integrationSystems) or Workday SOAP-style\n      PascalCase_With_Underscores (e.g. /Human_Resources/Get_Workers). No spaces,\n      hyphens, or other special characters.\n    message: 'Path \"{{property}}\" contains disallowed characters.'\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(/[A-Za-z][A-Za-z0-9_]*|/\\\\{[A-Za-z][A-Za-z0-9]*\\\\})+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash (except the root).\n    message: 'Path \"{{property}}\" should not end with a trailing slash.'\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  paths-no-query-strings:\n\
  \    description: Path templates must not include query strings.\n    message: 'Path \"{{property}}\" must not contain \"?\" — use parameters instead.'\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  paths-no-file-extensions:\n    description: Paths should not include file extensions.\n    message: 'Path \"{{property}}\" should not include a file extension.'\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\.(json|xml|yaml|yml)$\"\n\n  # ===========================================================================\n  # OPERATIONS\n  # ===========================================================================\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    message: \"Operation summary is required.\"\n    severity: error\n    given:\
  \ \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-workday-studio-prefix:\n    description: Operation summaries should begin with \"Workday Studio \".\n    message: 'Operation summary should start with \"Workday Studio \" (got \"{{value}}\").'\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday Studio\\\\s+\\\\S\"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    message: \"Operation description is required.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-operationId-required:\n    description: Every operation must have an operationId.\n    message: \"operationId is required.\"\n    severity: error\n    given:\
  \ \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camelcase:\n    description: operationId must be camelCase.\n    message: 'operationId \"{{value}}\" must be camelCase.'\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-operationId-verb-prefix:\n    description: >-\n      operationId should begin with an approved verb prefix (get, list, create,\n      update, delete, launch, search).\n    message: 'operationId \"{{value}}\" should start with get/list/create/update/delete/launch/search.'\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(get|list|create|update|delete|launch|search)[A-Z]\"\n\n  operation-tags-required:\n\
  \    description: Every operation must declare at least one tag.\n    message: \"Operation must include tags.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: tags\n      function: truthy\n\n  operation-tag-count:\n    description: Operation tags array must not be empty.\n    message: \"Operation tags array must not be empty.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  # ===========================================================================\n  # TAGS\n  # ===========================================================================\n\n  tags-defined-globally:\n    description: A top-level tags array must be defined.\n    message: \"Global tags array must be defined.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\n  tags-name-required:\n   \
  \ description: Every tag must have a name.\n    message: \"tag.name is required.\"\n    severity: error\n    given: \"$.tags[*]\"\n    then:\n      field: name\n      function: truthy\n\n  tags-description-required:\n    description: Every tag must have a description.\n    message: \"tag.description is required.\"\n    severity: warn\n    given: \"$.tags[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tags-title-case:\n    description: >-\n      Tag names should use Title Case (e.g. \"Integration Assemblies\",\n      \"Human Resources\", \"Benefits Administration\").\n    message: 'Tag name \"{{value}}\" should use Title Case.'\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z]*( [A-Z][A-Za-z]*)*$\"\n\n  operation-tags-must-be-defined-globally:\n    description: Every tag referenced on an operation must be defined in the global tags array.\n    message: 'Operation tag \"\
  {{value}}\" is not declared in the top-level tags array.'\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Integration Assemblies\n          - Integration Events\n          - Integration Systems\n          - Integration Templates\n          - Launch Parameters\n          - Absence Management\n          - Benefits Administration\n          - Compensation\n          - Financial Management\n          - Human Resources\n          - Payroll\n          - Recruiting\n          - Service Directory\n          - Staffing\n          - Time Tracking\n\n  # ===========================================================================\n  # PARAMETERS\n  # ===========================================================================\n\n  parameter-description-required:\n    description: Every parameter must have a description.\n    message: \"Parameter description is\
  \ required.\"\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-name-camelcase:\n    description: >-\n      Parameter names should use camelCase. The path identifier \"ID\" is\n      permitted as the canonical Workday resource identifier.\n    message: 'Parameter name \"{{value}}\" should be camelCase.'\n    severity: warn\n    given: \"$..parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([a-z][a-zA-Z0-9]*|ID)$\"\n\n  parameter-no-apikey-in-query:\n    description: API keys must not be passed as query parameters.\n    message: 'Parameter \"{{value}}\" looks like an API key in the query string — use a header.'\n    severity: error\n    given: \"$..parameters[?(@.in == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"(?i)^(api[-_]?key|access[-_]?token|auth[-_]?token)$\"\n\n  parameter-pagination-uses-limit-offset:\n\
  \    description: >-\n      Standardize pagination on limit/offset. The web services spec uses\n      pageSize/page; new operations should adopt limit/offset.\n    message: 'Pagination parameter \"{{value}}\" should be \"limit\" or \"offset\" — pageSize/page is discouraged.'\n    severity: warn\n    given: \"$..parameters[?(@.in == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(pageSize|page|page_size|page_number|per_page)$\"\n\n  # ===========================================================================\n  # REQUEST BODIES\n  # ===========================================================================\n\n  request-body-json-content:\n    description: Request bodies must support application/json.\n    message: \"Request body must declare application/json content.\"\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-description-recommended:\n\
  \    description: Request bodies should include a description.\n    message: \"Request body should have a description.\"\n    severity: info\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  # ===========================================================================\n  # RESPONSES\n  # ===========================================================================\n\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    message: \"Operation must define a 2xx success response.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2[0-9][0-9]$\":\n              type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required:\
  \ [\"202\"]\n            - required: [\"204\"]\n\n  response-401-required:\n    description: Operations should declare a 401 response since the API requires authentication.\n    message: \"Operation should declare a 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  response-403-recommended:\n    description: Operations should declare a 403 response for permission errors.\n    message: \"Operation should declare a 403 Forbidden response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses\"\n    then:\n      field: \"403\"\n      function: truthy\n\n  response-404-on-id-paths:\n    description: Operations on /{ID} paths should declare a 404 response.\n    message: \"Operation on a templated path should declare a 404 response.\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/\\\\{[A-Za-z]+\\\\\
  }/))][get,post,put,patch,delete].responses\"\n    then:\n      field: \"404\"\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description.\n    message: \"Response description is required.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  response-2xx-json-content:\n    description: 2xx responses must return application/json.\n    message: \"2xx response must declare application/json content.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses[?(@property.match(/^2[0-9][0-9]$/))].content\"\n    then:\n      field: application/json\n      function: truthy\n\n  response-error-schema-has-message:\n    description: The shared ErrorResponse schema should expose a message-bearing field.\n    message: \"ErrorResponse should expose at least one of: error, message, errors.\"\n\
  \    severity: warn\n    given: \"$.components.schemas.ErrorResponse.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"error\"]\n            - required: [\"message\"]\n            - required: [\"errors\"]\n\n  response-list-uses-total-data-wrapper:\n    description: >-\n      Collection responses should use the standard {total, data[]} wrapper\n      shape used throughout the Workday Studio specs.\n    message: \"Collection response schema should expose 'total' and 'data' properties.\"\n    severity: warn\n    given: \"$.components.schemas[?(@property.match(/Response$/))].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          allOf:\n            - required: [\"data\"]\n\n  # ===========================================================================\n  # SCHEMAS — PROPERTY NAMING\n  # ===========================================================================\n\
  \n  schema-property-name-camelcase:\n    description: >-\n      Schema property names should use camelCase. The canonical \"ID\" path\n      identifier is permitted at any depth.\n    message: 'Property name \"{{property}}\" should be camelCase.'\n    severity: warn\n    given: \"$.components.schemas..properties\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^([a-z][a-zA-Z0-9]*|ID)$\"\n\n  schema-id-property-name:\n    description: >-\n      Resource identifier properties should be named \"id\" (lowercase), matching\n      the convention used across the Workday Studio specs.\n    message: 'Use \"id\" rather than \"{{property}}\" for resource identifiers.'\n    severity: warn\n    given: \"$.components.schemas..properties\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"^(Id|ID|_id|identifier)$\"\n\n  schema-timestamp-property-suffix:\n    description: >-\n      Date-time properties\
  \ should be named with a \"DateTime\" suffix\n      (e.g. startDateTime, endDateTime, lastRunDateTime).\n    message: 'date-time property \"{{property}}\" should end with \"DateTime\".'\n    severity: info\n    given: \"$.components.schemas..properties[?(@.format == 'date-time')]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"DateTime$\"\n\n  schema-date-property-suffix:\n    description: >-\n      Date-only properties should be named with a \"Date\" suffix\n      (e.g. hireDate, startDate, effectiveDate).\n    message: 'date property \"{{property}}\" should end with \"Date\".'\n    severity: info\n    given: \"$.components.schemas..properties[?(@.format == 'date')]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"Date$\"\n\n  schema-top-level-description:\n    description: Top-level schemas in components should include a description.\n    message: 'Schema \"{{property}}\" should include a description.'\n    severity: info\n\
  \    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-type-required:\n    description: Every schema definition should declare a type.\n    message: \"Schema should declare a type.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # ===========================================================================\n  # SECURITY\n  # ===========================================================================\n\n  security-global-defined:\n    description: A global security requirement must be defined.\n    message: \"Global security must be defined.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  security-schemes-defined:\n    description: components.securitySchemes must be defined.\n    message: \"components.securitySchemes must be defined.\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field:\
  \ securitySchemes\n      function: truthy\n\n  security-oauth2-required:\n    description: Specs must define an OAuth2 security scheme named \"OAuth2\".\n    message: 'A security scheme named \"OAuth2\" must be defined.'\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: OAuth2\n      function: truthy\n\n  security-oauth2-flow-authorization-code:\n    description: The OAuth2 scheme must declare an authorizationCode flow.\n    message: \"OAuth2 must declare an authorizationCode flow.\"\n    severity: warn\n    given: \"$.components.securitySchemes.OAuth2.flows\"\n    then:\n      field: authorizationCode\n      function: truthy\n\n  security-oauth2-token-url-tenant:\n    description: OAuth2 tokenUrl should template the tenant in the path.\n    message: 'OAuth2 tokenUrl should include \"{tenant}\" (got \"{{value}}\").'\n    severity: info\n    given: \"$.components.securitySchemes.OAuth2.flows.authorizationCode.tokenUrl\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  security-scope-naming:\n    description: >-\n      OAuth2 scope names should use the Workday Studio convention of\n      \"<r|w>:<resource>\" (e.g. r:integrations, w:integrations, r:wws, w:wws).\n    message: 'Scope \"{{property}}\" should match \"<r|w>:<resource>\".'\n    severity: warn\n    given: \"$.components.securitySchemes.OAuth2.flows.authorizationCode.scopes\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^[rw]:[a-z][a-z0-9_]*$\"\n\n  # ===========================================================================\n  # HTTP METHOD CONVENTIONS\n  # ===========================================================================\n\n  no-request-body-on-get:\n    description: GET operations must not declare a request body.\n    message: \"GET operations must not have a requestBody.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field:\
  \ requestBody\n      function: falsy\n\n  no-request-body-on-delete:\n    description: DELETE operations should not declare a request body.\n    message: \"DELETE operations should not have a requestBody.\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  put-patch-request-body-required:\n    description: PUT and PATCH operations must declare a request body.\n    message: \"PUT/PATCH operations should declare a requestBody.\"\n    severity: warn\n    given: \"$.paths[*][put,patch]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # ===========================================================================\n  # GENERAL QUALITY\n  # ===========================================================================\n\n  no-empty-descriptions:\n    description: Description fields, when present, must not be empty strings.\n    message: \"Empty description is not allowed.\"\n    severity: error\n    given: \"$..description\"\
  \n    then:\n      function: truthy\n\n  external-docs-encouraged:\n    description: A top-level externalDocs object is encouraged for discoverability.\n    message: \"Consider adding a top-level externalDocs entry.\"\n    severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n\n  examples-encouraged:\n    description: Adding examples to schemas helps consumers understand payloads.\n    message: 'Schema \"{{property}}\" has no example or examples — consider adding one.'\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"example\"]\n            - required: [\"examples\"]\n\n  deprecation-must-be-documented:\n    description: Deprecated operations must explain the deprecation in their description.\n    message: 'Deprecated operation should mention \"deprecat\" in its description.'\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options][?(@.deprecated\
  \ == true)].description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)deprecat\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-studio/refs/heads/main/rules/workday-studio-spectral-rules.yml
tags:
- Cloud
- Development
- Enterprise
- Finance
- HR
- IDE
- Integration
- Spectral
- Linting
- API Governance
---
