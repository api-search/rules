---
api_specs:
- filename: fastdol-openapi.yml
  format: yaml
  label: FastDOL API
  slug: fastdol-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fastdol/main/openapi/fastdol-openapi.yml
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
description: Spectral linting rules defining API design standards and conventions for FastDOL.
layout: rules
name: FastDOL API Rules
provider_name: FastDOL
provider_slug: fastdol
rule_count: 32
rules:
- description: API title must start with "FastDOL".
  given: $.info.title
  name: info-title-fastdol-prefix
  severity: error
- description: info.description is required and must be at least 40 characters.
  given: $.info
  name: info-description-required
  severity: warn
- description: info.version is required.
  given: $.info
  name: info-version-required
  severity: error
- description: info.contact.email should be present.
  given: $.info
  name: info-contact-email
  severity: warn
- description: info.termsOfService should be present.
  given: $.info
  name: info-terms-of-service
  severity: info
- description: OpenAPI version must be 3.0.x or 3.1.x.
  given: $.openapi
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Production server URL should be api.fastdol.com.
  given: $.servers[*].url
  name: servers-fastdol-host
  severity: warn
- description: Public data paths must be prefixed with /v1/ (auth, dashboard, webhooks excepted).
  given: $.paths[?(!@property.match(/^\/(auth|dashboard|webhooks)\b/))]~
  name: paths-version-prefix
  severity: warn
- description: Path segments must be lower-case kebab-case (snake_case forbidden).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Path must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Every operation must declare an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: operationId must be snake_case (FastAPI default).
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-operationid-snake-case
  severity: warn
- description: Every operation must declare a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: warn
- description: Operation summary must be Title Case and prefixed with "FastDOL".
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-fastdol-prefix
  severity: warn
- description: Every operation should be tagged.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Operation should declare x-microcks-operation for mock-server compatibility.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-microcks-extension
  severity: info
- description: Every parameter must declare a description.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameter names must be snake_case.
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in!='header')]
  name: parameter-snake-case
  severity: warn
- description: Pagination must use the offset/limit pair (no page/per_page).
  given: $.paths[*][get,post,put,delete,patch].parameters[*].name
  name: parameter-pagination-offset-limit
  severity: warn
- description: Request bodies must offer application/json (multipart for upload only).
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content
  severity: warn
- description: Every operation must declare a 2xx success response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Operations behind auth (X-Api-Key) should declare a 401 response.
  given: $.paths[?(!@property.match(/^\/(auth|webhooks|v1\/health|v1\/sitemap)\b/))][get,post,put,delete,patch].responses
  name: response-401-on-protected
  severity: warn
- description: Data endpoints should declare a 429 rate-limit response.
  given: $.paths[?(@property.match(/^\/v1\//))][get,post].responses
  name: response-429-rate-limit
  severity: info
- description: Operations with parameters should declare a 422 validation response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-422-validation
  severity: info
- description: Responses must use application/json.
  given: $.paths[*][get,post,put,delete,patch].responses[*].content
  name: response-json-content
  severity: warn
- description: Schema properties must be snake_case.
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: warn
- description: Identifier properties must end in _id (e.g. employer_id, job_id, key_id).
  given: $.components.schemas[*].properties[?(@property.match(/(Id|ID|^id)$/))]~
  name: schema-id-property-naming
  severity: info
- description: Auth must be the X-Api-Key header (FastDOL convention).
  given: $.components.securitySchemes[*]
  name: security-x-api-key-header
  severity: warn
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-description
  severity: warn
- description: Responses are encouraged to include named examples (Microcks-compatible).
  given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]
  name: operation-examples-encouraged
  severity: info
rules_file: rules/fastdol-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/fastdol/refs/heads/main/rules/fastdol-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 6
  warn: 18
slug: fastdol-rules
source_filename: fastdol-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# FastDOL Spectral Ruleset\n# Enforces the conventions observed in the FastDOL OpenAPI specification\n# (FastAPI-generated, snake_case paths and properties, X-Api-Key header auth, /v1 prefix).\n# Apply with: spectral lint -r rules/fastdol-rules.yml openapi/fastdol-openapi.yml\n\nextends: spectral:oas\n\nrules:\n  # ============================================================\n  # INFO / METADATA\n  # ============================================================\n  info-title-fastdol-prefix:\n    description: API title must start with \"FastDOL\".\n    message: '{{property}} must start with \"FastDOL\".'\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^FastDOL'\n\n  info-description-required:\n    description: info.description is required and must be at least 40 characters.\n    message: '{{property}} must be present and meaningful.'\n    severity: warn\n    given: $.info\n    then:\n      - field: description\n\
  \        function: truthy\n      - field: description\n        function: length\n        functionOptions:\n          min: 40\n\n  info-version-required:\n    description: info.version is required.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-email:\n    description: info.contact.email should be present.\n    severity: warn\n    given: $.info\n    then:\n      field: contact.email\n      function: truthy\n\n  info-terms-of-service:\n    description: info.termsOfService should be present.\n    severity: info\n    given: $.info\n    then:\n      field: termsOfService\n      function: truthy\n\n  # ============================================================\n  # OPENAPI VERSION\n  # ============================================================\n  openapi-version-3:\n    description: OpenAPI version must be 3.0.x or 3.1.x.\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: '^3\\.[01]\\.\\d+$'\n\n  # ============================================================\n  # SERVERS\n  # ============================================================\n  servers-required:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  servers-fastdol-host:\n    description: Production server URL should be api.fastdol.com.\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: 'fastdol\\.com'\n\n  # ============================================================\n  # PATHS — NAMING CONVENTIONS\n  # ============================================================\n  paths-version-prefix:\n    description:\
  \ 'Public data paths must be prefixed with /v1/ (auth, dashboard, webhooks excepted).'\n    severity: warn\n    given: $.paths[?(!@property.match(/^\\/(auth|dashboard|webhooks)\\b/))]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/v1/'\n\n  paths-kebab-case:\n    description: Path segments must be lower-case kebab-case (snake_case forbidden).\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z0-9-]+|/\\{[a-z_][a-z0-9_]*\\})+$'\n\n  paths-no-trailing-slash:\n    description: Path must not end with a trailing slash.\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '.+/$'\n\n  # ============================================================\n  # OPERATIONS\n  # ============================================================\n  operation-operationid-required:\n    description: Every operation must declare an operationId.\n\
  \    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-snake-case:\n    description: operationId must be snake_case (FastAPI default).\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  operation-summary-required:\n    description: Every operation must declare a summary.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-fastdol-prefix:\n    description: Operation summary must be Title Case and prefixed with \"FastDOL\".\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^FastDOL\\s'\n\n  operation-tags-required:\n    description: Every operation should be\
  \ tagged.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  operation-microcks-extension:\n    description: Operation should declare x-microcks-operation for mock-server compatibility.\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  # ============================================================\n  # PARAMETERS\n  # ============================================================\n  parameter-description-required:\n    description: Every parameter must declare a description.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-snake-case:\n    description: Parameter names must be snake_case.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in!='header')]\n    then:\n      field:\
  \ name\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  parameter-pagination-offset-limit:\n    description: Pagination must use the offset/limit pair (no page/per_page).\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '^(page|per_page|page_size|pageSize|cursor)$'\n\n  # ============================================================\n  # REQUEST BODIES\n  # ============================================================\n  request-body-json-content:\n    description: Request bodies must offer application/json (multipart for upload only).\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['application/json']\n            - required: ['multipart/form-data']\n\n  # ============================================================\n\
  \  # RESPONSES\n  # ============================================================\n  response-success-required:\n    description: Every operation must declare a 2xx success response.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['202']\n            - required: ['204']\n\n  response-401-on-protected:\n    description: Operations behind auth (X-Api-Key) should declare a 401 response.\n    severity: warn\n    given: \"$.paths[?(!@property.match(/^\\\\/(auth|webhooks|v1\\\\/health|v1\\\\/sitemap)\\\\b/))][get,post,put,delete,patch].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  response-429-rate-limit:\n    description: Data endpoints should declare a 429 rate-limit response.\n    severity: info\n    given: $.paths[?(@property.match(/^\\/v1\\//))][get,post].responses\n\
  \    then:\n      field: '429'\n      function: truthy\n\n  response-422-validation:\n    description: Operations with parameters should declare a 422 validation response.\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      field: '422'\n      function: truthy\n\n  response-json-content:\n    description: Responses must use application/json.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*].content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['application/json']\n            - required: ['text/csv']\n            - required: ['application/pdf']\n\n  # ============================================================\n  # SCHEMAS — PROPERTY NAMING\n  # ============================================================\n  schema-property-snake-case:\n    description: Schema properties must be snake_case.\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  schema-id-property-naming:\n    description: Identifier properties must end in _id (e.g. employer_id, job_id, key_id).\n    severity: info\n    given: \"$.components.schemas[*].properties[?(@property.match(/(Id|ID|^id)$/))]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: '_id$'\n\n  # ============================================================\n  # SECURITY\n  # ============================================================\n  security-x-api-key-header:\n    description: Auth must be the X-Api-Key header (FastDOL convention).\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type: { const: 'apiKey' }\n            in: { const: 'header' }\n            name: { const: 'X-Api-Key' }\n\n  # ============================================================\n\
  \  # GENERAL QUALITY\n  # ============================================================\n  no-empty-description:\n    description: Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: truthy\n\n  operation-examples-encouraged:\n    description: Responses are encouraged to include named examples (Microcks-compatible).\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].responses[*].content[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['example']\n            - required: ['examples']\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/fastdol/refs/heads/main/rules/fastdol-rules.yml
tags:
- OSHA
- Compliance
- Workplace Safety
- Public Records
- Federal Enforcement
- Labor
- Spectral
- Linting
- API Governance
---
