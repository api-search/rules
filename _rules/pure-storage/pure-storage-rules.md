---
api_specs:
- filename: flasharray-rest-api-openapi.yml
  format: yaml
  label: FlashArray REST API
  slug: flasharray-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/pure-storage/refs/heads/main/openapi/flasharray-rest-api-openapi.yml
- filename: flashblade-rest-api-openapi.yml
  format: yaml
  label: FlashBlade REST API
  slug: flashblade-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/pure-storage/refs/heads/main/openapi/flashblade-rest-api-openapi.yml
- filename: pure1-cloud-api-openapi.yml
  format: yaml
  label: Pure1 Public REST API
  slug: pure1-cloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/pure-storage/refs/heads/main/openapi/pure1-cloud-api-openapi.yml
categories:
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
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for Pure Storage.
layout: rules
name: Pure Storage API Rules
provider_name: Pure Storage
provider_slug: pure-storage
rule_count: 26
rules:
- description: API title should reflect the Pure Storage product family (e.g. "FlashArray REST API", "FlashBlade REST API", "Pure1 Public REST API").
  given: $.info.title
  name: info-title-pure-storage-prefix
  severity: warn
- description: API info.description must be present and non-trivial.
  given: $.info
  name: info-description-required
  severity: error
- description: API version should be either semver or major.minor (e.g. 2.52, 1.5).
  given: $.info.version
  name: info-version-semver-or-major-minor
  severity: warn
- description: Pure Storage specs are OpenAPI 3.0.x.
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Path segments use snake_case (matches Pure Storage convention; e.g. /api/2.52/active-directory, /arrays/cloud-provider-tags).
  given: $.paths.*~
  name: paths-snake-case-segments
  severity: warn
- description: Resource paths should be version-prefixed (e.g. /api/2.52/, /1.5/, /oauth2/1.0/).
  given: $.paths.*~
  name: paths-version-prefix
  severity: warn
- description: Path entries must not have a trailing slash.
  given: $.paths.*~
  name: paths-no-trailing-slash
  severity: error
- description: Every operation must have a summary.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should begin with "Pure Storage" to clearly identify the provider.
  given: $.paths.*[get,post,put,patch,delete,head,options].summary
  name: operation-summary-pure-storage-prefix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: operation-operationId-required
  severity: error
- description: Every operation must include at least one tag.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Tags should be declared at the document root with descriptions (Pure Storage specs declare 50+ resource tags globally).
  given: $
  name: tags-defined-globally
  severity: warn
- description: Tag names should use Title Case (e.g. "Active Directory", "Alert Watchers", "API Clients").
  given: $.tags[*].name
  name: tag-title-case
  severity: warn
- description: Query and path parameter names should use snake_case (Pure Storage uses snake_case for filters, names, ids, etc.).
  given: $.paths.*[get,post,put,patch,delete,head,options].parameters[?(@.in=='query' || @.in=='path')].name
  name: parameter-snake-case
  severity: warn
- description: All parameters must have a description.
  given: $.paths.*[get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: When session-based auth is used, FA/FB exposes 'x-auth-token' as the auth header.
  given: $.paths.*[get,post,put,patch,delete,head,options].parameters[?(@.in=='header' && @.name=='x-auth-token')]
  name: parameter-x-auth-token-header
  severity: info
- description: Every operation must define at least one 2xx response.
  given: $.paths.*[get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: Mutating operations should document a 400 Bad Request response.
  given: $.paths.*[post,put,patch,delete].responses
  name: response-400-recommended
  severity: info
- description: Responses should serve application/json.
  given: $.paths.*[get,post,put,patch,delete].responses.*.content
  name: response-application-json
  severity: warn
- description: Schema property names should be snake_case (Pure Storage uses snake_case across FA/FB/Pure1 schemas).
  given: $.components.schemas.*.properties.*~
  name: schema-property-snake-case
  severity: warn
- description: Object identifier 'id' should be a string (Pure Storage uses opaque string ids).
  given: $.components.schemas.*.properties.id
  name: schema-id-property-string
  severity: info
- description: Time-valued properties should be named '*_time' or '*_at' (e.g. created, updated).
  given: $.components.schemas.*.properties[?(@.format=='date-time')]~
  name: schema-time-property-pattern
  severity: info
- description: Authentication mechanism should be documented (FA/FB use OAuth 2.0 token-exchange JWTs and a session 'x-auth-token' header; Pure1 uses OAuth 2.0 token exchange).
  given: $
  name: security-defined
  severity: warn
- description: Request bodies should accept application/json.
  given: $.paths.*[post,put,patch].requestBody.content
  name: request-body-application-json
  severity: warn
- description: Descriptions, when present, must not be empty strings.
  given: $..description
  name: no-empty-description
  severity: warn
rules_file: rules/pure-storage-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/pure-storage/refs/heads/main/rules/pure-storage-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 4
  warn: 14
slug: pure-storage-rules
source_filename: pure-storage-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# Pure Storage Spectral Ruleset\n#\n# Opinionated Spectral rules derived from the Pure Storage FlashArray, FlashBlade,\n# and Pure1 Public REST API OpenAPI specifications. These rules enforce the\n# patterns observed across the official specs and a few common-sense API quality\n# rules layered on top.\n#\n# Source specs:\n#   openapi/flasharray-rest-api-openapi.yml   (FA 2.52)\n#   openapi/flashblade-rest-api-openapi.yml   (FB 2.26)\n#   openapi/pure1-cloud-api-openapi.yml       (Pure1 1.5)\n\nextends: spectral:oas\n\nformats:\n  - oas3\n\nrules:\n\n  # ----------------------------------------------------------------------------\n  # INFO / METADATA\n  # ----------------------------------------------------------------------------\n\n  info-title-pure-storage-prefix:\n    description: API title should reflect the Pure Storage product family (e.g. \"FlashArray REST API\", \"FlashBlade REST API\", \"Pure1 Public REST API\").\n    message: \"Title '{{value}}' should reference a\
  \ Pure Storage product (FlashArray, FlashBlade, or Pure1).\"\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(FlashArray|FlashBlade|Pure1|Pure Storage)\"\n\n  info-description-required:\n    description: API info.description must be present and non-trivial.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-semver-or-major-minor:\n    description: API version should be either semver or major.minor (e.g. 2.52, 1.5).\n    severity: warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[0-9]+\\\\.[0-9]+(\\\\.[0-9]+)?$\"\n\n  # ----------------------------------------------------------------------------\n  # OPENAPI VERSION\n  # ----------------------------------------------------------------------------\n\n  openapi-version-3:\n    description: Pure Storage specs are OpenAPI 3.0.x.\n    severity:\
  \ error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # ----------------------------------------------------------------------------\n  # SERVERS\n  # ----------------------------------------------------------------------------\n\n  servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n  # PATHS — NAMING CONVENTIONS\n  # ----------------------------------------------------------------------------\n\n  paths-snake-case-segments:\n    description: Path segments use snake_case (matches Pure Storage convention; e.g. /api/2.52/active-directory, /arrays/cloud-provider-tags).\n    message: \"Path segment in '{{value}}' should be snake_case or kebab-case (lowercase only).\"\n    severity: warn\n    given: $.paths.*~\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^/([a-z0-9_./{}-]+)?$\"\n\n  paths-version-prefix:\n    description: Resource paths should be version-prefixed (e.g. /api/2.52/, /1.5/, /oauth2/1.0/).\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(api/[0-9]+\\\\.[0-9]+|oauth2/[0-9]+\\\\.[0-9]+|[0-9]+\\\\.[0-9]+)/\"\n\n  paths-no-trailing-slash:\n    description: Path entries must not have a trailing slash.\n    severity: error\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # ----------------------------------------------------------------------------\n  # OPERATIONS\n  # ----------------------------------------------------------------------------\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n\
  \      field: summary\n      function: truthy\n\n  operation-summary-pure-storage-prefix:\n    description: Operation summaries should begin with \"Pure Storage\" to clearly identify the provider.\n    message: 'Summary \"{{value}}\" should start with \"Pure Storage\".'\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Pure Storage \"\n\n  operation-operationId-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must include at least one tag.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n\
  \  # TAGS\n  # ----------------------------------------------------------------------------\n\n  tags-defined-globally:\n    description: Tags should be declared at the document root with descriptions (Pure Storage specs declare 50+ resource tags globally).\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tag-title-case:\n    description: Tag names should use Title Case (e.g. \"Active Directory\", \"Alert Watchers\", \"API Clients\").\n    message: 'Tag name \"{{value}}\" should use Title Case.'\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z0-9][A-Za-z0-9 /+-]*$\"\n\n  # ----------------------------------------------------------------------------\n  # PARAMETERS\n  # ----------------------------------------------------------------------------\n\n  parameter-snake-case:\n    description: Query and path parameter names should use snake_case (Pure Storage uses snake_case\
  \ for filters, names, ids, etc.).\n    message: 'Parameter name \"{{value}}\" should be snake_case.'\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options].parameters[?(@.in=='query' || @.in=='path')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-x-auth-token-header:\n    description: When session-based auth is used, FA/FB exposes 'x-auth-token' as the auth header.\n    severity: info\n    given: $.paths.*[get,post,put,patch,delete,head,options].parameters[?(@.in=='header' && @.name=='x-auth-token')]\n    then:\n      field: name\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n  #\
  \ RESPONSES\n  # ----------------------------------------------------------------------------\n\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options].responses\n    then:\n      function: truthy\n\n  response-400-recommended:\n    description: Mutating operations should document a 400 Bad Request response.\n    severity: info\n    given: $.paths.*[post,put,patch,delete].responses\n    then:\n      field: \"400\"\n      function: truthy\n\n  response-application-json:\n    description: Responses should serve application/json.\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete].responses.*.content\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n  # SCHEMAS — PROPERTY NAMING\n  # ----------------------------------------------------------------------------\n\
  \n  schema-property-snake-case:\n    description: Schema property names should be snake_case (Pure Storage uses snake_case across FA/FB/Pure1 schemas).\n    message: 'Property name \"{{property}}\" should be snake_case.'\n    severity: warn\n    given: $.components.schemas.*.properties.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  schema-id-property-string:\n    description: Object identifier 'id' should be a string (Pure Storage uses opaque string ids).\n    severity: info\n    given: $.components.schemas.*.properties.id\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  schema-time-property-pattern:\n    description: Time-valued properties should be named '*_time' or '*_at' (e.g. created, updated).\n    severity: info\n    given: $.components.schemas.*.properties[?(@.format=='date-time')]~\n    then:\n      function: pattern\n      functionOptions:\n \
  \       match: \"(_time|_at|created|updated|modified)$\"\n\n  # ----------------------------------------------------------------------------\n  # SECURITY\n  # ----------------------------------------------------------------------------\n\n  security-defined:\n    description: Authentication mechanism should be documented (FA/FB use OAuth 2.0 token-exchange JWTs and a session 'x-auth-token' header; Pure1 uses OAuth 2.0 token exchange).\n    severity: warn\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n  # REQUEST BODY\n  # ----------------------------------------------------------------------------\n\n  request-body-application-json:\n    description: Request bodies should accept application/json.\n    severity: warn\n    given: $.paths.*[post,put,patch].requestBody.content\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  # ----------------------------------------------------------------------------\n\
  \  # GENERAL QUALITY\n  # ----------------------------------------------------------------------------\n\n  no-empty-description:\n    description: Descriptions, when present, must not be empty strings.\n    severity: warn\n    given: $..description\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/pure-storage/refs/heads/main/rules/pure-storage-rules.yml
tags:
- Storage
- Data Storage
- Flash Storage
- Enterprise Storage
- Cloud Storage
- Object Storage
- File Storage
- Block Storage
- Kubernetes Storage
- Infrastructure
- Spectral
- Linting
- API Governance
---
