---
api_specs:
- filename: dexcom-dexcom-api.yml
  format: yaml
  label: Dexcom Developer API
  slug: dexcom-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dexcom/refs/heads/main/openapi/dexcom-dexcom-api.yml
categories:
- info
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for Dexcom.
layout: rules
name: Dexcom API Rules
provider_name: Dexcom
provider_slug: dexcom
rule_count: 37
rules:
- description: Every API must have a title in the info object.
  given: $.info
  name: info-title-required
  severity: error
- description: Titles should start with "Dexcom" for portfolio consistency.
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: The info object must include a description explaining the API purpose.
  given: $.info
  name: info-description-required
  severity: error
- description: Info descriptions should be at least 80 characters to be meaningful.
  given: $.info.description
  name: info-description-min-length
  severity: warn
- description: A version string is required in the info object (e.g. v3).
  given: $.info
  name: info-version-required
  severity: error
- description: API version should match the v{N} pattern Dexcom uses (v2, v3).
  given: $.info.version
  name: info-version-format
  severity: warn
- description: Specs must declare OpenAPI 3.x.
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: At least one server must be declared.
  given: $.servers
  name: servers-required
  severity: error
- description: All Dexcom server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Server URLs should point to a Dexcom-controlled host (api.dexcom.com, api.dexcom.eu, api.dexcom.jp, sandbox-api.dexcom.com).
  given: $.servers[*].url
  name: servers-dexcom-host
  severity: warn
- description: Each server must include a description (e.g. Production, Sandbox).
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Paths should be versioned with a /v{N}/ prefix as Dexcom does.
  given: $.paths.*~
  name: paths-versioned
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths.*~
  name: paths-no-trailing-slash
  severity: error
- description: Paths must not embed query strings; use parameters instead.
  given: $.paths.*~
  name: paths-no-query-string
  severity: error
- description: Path segments should use lowerCamelCase (e.g. dataRange) consistent with Dexcom's API.
  given: $.paths.*~
  name: paths-lower-camel-case
  severity: warn
- description: Every operation must define an operationId.
  given: $.paths.*[get,put,post,delete,patch,options,head]
  name: operation-operationId-required
  severity: error
- description: operationIds must be camelCase (e.g. getEgvsV3, exchangeAuthorizationCode).
  given: $.paths.*[get,put,post,delete,patch,options,head].operationId
  name: operation-operationId-camel-case
  severity: warn
- description: Every operation must have a summary.
  given: $.paths.*[get,put,post,delete,patch,options,head]
  name: operation-summary-required
  severity: error
- description: Summaries should be Title Case (each significant word capitalized).
  given: $.paths.*[get,put,post,delete,patch,options,head].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation should include a description.
  given: $.paths.*[get,put,post,delete,patch,options,head]
  name: operation-description-required
  severity: warn
- description: Operations must declare at least one tag for documentation grouping.
  given: $.paths.*[get,put,post,delete,patch,options,head]
  name: operation-tags-required
  severity: warn
- description: A global tags array should be defined at the spec level.
  given: $
  name: tags-defined
  severity: info
- description: Tag names should be Title Case (e.g. "Estimated Glucose Values").
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: Each declared tag should have a description.
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: Parameters must include a description.
  given: $.paths.*.*.parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameter names should use lowerCamelCase (e.g. startDate, endDate, lastSyncTime, client_id is permitted only for OAuth bodies).
  given: $.paths.*.*.parameters[?(@.in!='header')].name
  name: parameter-camel-case
  severity: warn
- description: startDate and endDate query parameters must be defined as date-time strings.
  given: $.paths.*.*.parameters[?(@.name=='startDate' || @.name=='endDate')]
  name: parameter-date-iso8601
  severity: error
- description: Every operation must define at least one 2xx response.
  given: $.paths.*[get,put,post,delete,patch,options,head].responses
  name: response-success-required
  severity: error
- description: Each response must have a description.
  given: $.paths.*.*.responses[*]
  name: response-description-required
  severity: warn
- description: 2xx responses should declare application/json content.
  given: $.paths.*.*.responses['200','201','202'].content
  name: response-application-json
  severity: warn
- description: Schema properties should use lowerCamelCase (systemTime, displayTime, transmitterId, transmitterGeneration).
  given: $.components.schemas.*.properties.*~
  name: schema-property-camel-case
  severity: warn
- description: Properties whose names end in "Time" or "Date" should declare format date-time.
  given: $.components.schemas.*.properties[?(@property.match(/(Time|Date)$/))]
  name: schema-datetime-format
  severity: info
- description: A global security requirement must be declared.
  given: $
  name: security-defined
  severity: error
- description: Dexcom uses OAuth 2.0; an OAuth2 security scheme must be defined.
  given: $.components.securitySchemes
  name: security-scheme-oauth2
  severity: error
- description: The OAuth2 scheme should expose the authorizationCode flow with offline_access scope.
  given: $.components.securitySchemes[?(@.type=='oauth2')]
  name: security-oauth2-authorization-code
  severity: warn
- description: Each operation should declare x-microcks-operation for mock-server compatibility.
  given: $.paths.*[get,put,post,delete,patch,options,head]
  name: operation-microcks-extension
  severity: info
- description: Successful JSON responses should include named examples for Microcks.
  given: $.paths.*.*.responses['200','201','202'].content.application/json
  name: response-named-examples
  severity: info
rules_file: rules/dexcom-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/dexcom/refs/heads/main/rules/dexcom-rules.yml
severity_counts:
  error: 14
  hint: 0
  info: 4
  warn: 19
slug: dexcom-rules
source_filename: dexcom-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# Dexcom Developer API — Spectral ruleset\n#\n# Enforces conventions observed in the Dexcom v3 OpenAPI specification:\n# - Title and summary prefix \"Dexcom ...\" / Title Case operation summaries\n# - camelCase operationIds with verb prefixes (get, exchange, refresh)\n# - Versioned, lowerCamelCase paths under /v3/users/self/{resource}\n# - OAuth 2.0 authorization-code security with offline_access scope\n# - ISO 8601 startDate/endDate query parameters\n# - camelCase JSON property naming (e.g. systemTime, displayTime, transmitterId)\n\nrules:\n\n  # ---------------------------------------------------------------------------\n  # INFO / METADATA\n  # ---------------------------------------------------------------------------\n\n  info-title-required:\n    description: Every API must have a title in the info object.\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-title-prefix:\n    description: Titles should start with \"\
  Dexcom\" for portfolio consistency.\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^Dexcom '\n\n  info-description-required:\n    description: The info object must include a description explaining the API purpose.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-description-min-length:\n    description: Info descriptions should be at least 80 characters to be meaningful.\n    severity: warn\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 80\n\n  info-version-required:\n    description: A version string is required in the info object (e.g. v3).\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-version-format:\n    description: API version should match the v{N} pattern Dexcom uses (v2, v3).\n    severity: warn\n    given: $.info.version\n   \
  \ then:\n      function: pattern\n      functionOptions:\n        match: '^v[0-9]+$'\n\n  # ---------------------------------------------------------------------------\n  # OPENAPI VERSION\n  # ---------------------------------------------------------------------------\n\n  openapi-version-3:\n    description: Specs must declare OpenAPI 3.x.\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: '^3\\.'\n\n  # ---------------------------------------------------------------------------\n  # SERVERS\n  # ---------------------------------------------------------------------------\n\n  servers-required:\n    description: At least one server must be declared.\n    severity: error\n    given: $.servers\n    then:\n      function: truthy\n\n  servers-https:\n    description: All Dexcom server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n      \
  \  match: '^https://'\n\n  servers-dexcom-host:\n    description: Server URLs should point to a Dexcom-controlled host (api.dexcom.com, api.dexcom.eu, api.dexcom.jp, sandbox-api.dexcom.com).\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://(sandbox-api|api)\\.dexcom\\.(com|eu|jp)$'\n\n  servers-description:\n    description: Each server must include a description (e.g. Production, Sandbox).\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # PATHS — NAMING CONVENTIONS\n  # ---------------------------------------------------------------------------\n\n  paths-versioned:\n    description: Paths should be versioned with a /v{N}/ prefix as Dexcom does.\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ '^/v[0-9]+/'\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '.+/$'\n\n  paths-no-query-string:\n    description: Paths must not embed query strings; use parameters instead.\n    severity: error\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '\\?'\n\n  paths-lower-camel-case:\n    description: Path segments should use lowerCamelCase (e.g. dataRange) consistent with Dexcom's API.\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z][a-zA-Z0-9]*|/v[0-9]+|/users|/self|/\\{[a-zA-Z]+\\})+$'\n\n  # ---------------------------------------------------------------------------\n  # OPERATIONS\n  # ---------------------------------------------------------------------------\n\n  operation-operationId-required:\n\
  \    description: Every operation must define an operationId.\n    severity: error\n    given: $.paths.*[get,put,post,delete,patch,options,head]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camel-case:\n    description: operationIds must be camelCase (e.g. getEgvsV3, exchangeAuthorizationCode).\n    severity: warn\n    given: $.paths.*[get,put,post,delete,patch,options,head].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths.*[get,put,post,delete,patch,options,head]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Summaries should be Title Case (each significant word capitalized).\n    severity: warn\n    given: $.paths.*[get,put,post,delete,patch,options,head].summary\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: '^[A-Z][A-Za-z0-9]*( [A-Z0-9][A-Za-z0-9/]*)*$'\n\n  operation-description-required:\n    description: Every operation should include a description.\n    severity: warn\n    given: $.paths.*[get,put,post,delete,patch,options,head]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must declare at least one tag for documentation grouping.\n    severity: warn\n    given: $.paths.*[get,put,post,delete,patch,options,head]\n    then:\n      field: tags\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # TAGS\n  # ---------------------------------------------------------------------------\n\n  tags-defined:\n    description: A global tags array should be defined at the spec level.\n    severity: info\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tags-title-case:\n    description: Tag names should be\
  \ Title Case (e.g. \"Estimated Glucose Values\").\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z0-9]*( [A-Z0-9][A-Za-z0-9]*)*$'\n\n  tag-description-required:\n    description: Each declared tag should have a description.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # PARAMETERS\n  # ---------------------------------------------------------------------------\n\n  parameter-description-required:\n    description: Parameters must include a description.\n    severity: warn\n    given: $.paths.*.*.parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-camel-case:\n    description: Parameter names should use lowerCamelCase (e.g. startDate, endDate, lastSyncTime, client_id is permitted only for OAuth bodies).\n    severity: warn\n\
  \    given: $.paths.*.*.parameters[?(@.in!='header')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9_]*$'\n\n  parameter-date-iso8601:\n    description: startDate and endDate query parameters must be defined as date-time strings.\n    severity: error\n    given: \"$.paths.*.*.parameters[?(@.name=='startDate' || @.name=='endDate')]\"\n    then:\n      field: schema.format\n      function: pattern\n      functionOptions:\n        match: '^date-time$'\n\n  # ---------------------------------------------------------------------------\n  # RESPONSES\n  # ---------------------------------------------------------------------------\n\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    severity: error\n    given: $.paths.*[get,put,post,delete,patch,options,head].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n\
  \            '^(2[0-9]{2}|3[0-9]{2})$':\n              type: object\n          minProperties: 1\n\n  response-description-required:\n    description: Each response must have a description.\n    severity: warn\n    given: $.paths.*.*.responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-application-json:\n    description: 2xx responses should declare application/json content.\n    severity: warn\n    given: \"$.paths.*.*.responses['200','201','202'].content\"\n    then:\n      field: application/json\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # SCHEMAS — PROPERTY NAMING\n  # ---------------------------------------------------------------------------\n\n  schema-property-camel-case:\n    description: Schema properties should use lowerCamelCase (systemTime, displayTime, transmitterId, transmitterGeneration).\n    severity: warn\n    given: $.components.schemas.*.properties.*~\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$|^(access_token|refresh_token|expires_in|token_type|client_id|client_secret|grant_type|redirect_uri|response_type)$'\n\n  schema-datetime-format:\n    description: Properties whose names end in \"Time\" or \"Date\" should declare format date-time.\n    severity: info\n    given: \"$.components.schemas.*.properties[?(@property.match(/(Time|Date)$/))]\"\n    then:\n      field: format\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # SECURITY\n  # ---------------------------------------------------------------------------\n\n  security-defined:\n    description: A global security requirement must be declared.\n    severity: error\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  security-scheme-oauth2:\n    description: Dexcom uses OAuth 2.0; an OAuth2 security scheme must be defined.\n    severity: error\n    given:\
  \ $.components.securitySchemes\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            '.*':\n              type: object\n              properties:\n                type:\n                  enum:\n                    - oauth2\n                    - http\n                    - apiKey\n\n  security-oauth2-authorization-code:\n    description: The OAuth2 scheme should expose the authorizationCode flow with offline_access scope.\n    severity: warn\n    given: $.components.securitySchemes[?(@.type=='oauth2')]\n    then:\n      field: flows.authorizationCode\n      function: truthy\n\n  # ---------------------------------------------------------------------------\n  # MICROCKS / EXAMPLES\n  # ---------------------------------------------------------------------------\n\n  operation-microcks-extension:\n    description: Each operation should declare x-microcks-operation for mock-server compatibility.\n   \
  \ severity: info\n    given: $.paths.*[get,put,post,delete,patch,options,head]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  response-named-examples:\n    description: Successful JSON responses should include named examples for Microcks.\n    severity: info\n    given: \"$.paths.*.*.responses['200','201','202'].content.application/json\"\n    then:\n      field: examples\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/dexcom/refs/heads/main/rules/dexcom-rules.yml
tags:
- Continuous Glucose Monitoring
- Diabetes
- Digital Health
- Glucose
- Healthcare
- Medical Devices
- Wearables
- Spectral
- Linting
- API Governance
---
