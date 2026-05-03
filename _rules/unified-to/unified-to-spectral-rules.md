---
api_specs:
- filename: unified-to-accounting-openapi.yaml
  format: yaml
  label: Unified.to Accounting API
  slug: accounting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-accounting-openapi.yaml
- filename: unified-to-marketing-openapi.yaml
  format: yaml
  label: Unified.to Advertising API
  slug: ads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-marketing-openapi.yaml
- filename: unified-to-hr-talent-openapi.yaml
  format: yaml
  label: Unified.to Assessment API
  slug: assessment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-hr-talent-openapi.yaml
- filename: unified-to-ats-openapi.yaml
  format: yaml
  label: Unified.to ATS API
  slug: ats-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-ats-openapi.yaml
- filename: unified-to-productivity-openapi.yaml
  format: yaml
  label: Unified.to Calendar & Meetings API
  slug: calendar-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-productivity-openapi.yaml
- filename: unified-to-it-ops-openapi.yaml
  format: yaml
  label: Unified.to Call Center API
  slug: call-center-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-it-ops-openapi.yaml
- filename: unified-to-crm-openapi.yaml
  format: yaml
  label: Unified.to CRM API
  slug: crm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-crm-openapi.yaml
- filename: unified-to-commerce-openapi.yaml
  format: yaml
  label: Unified.to E-Commerce API
  slug: ecommerce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-commerce-openapi.yaml
- filename: unified-to-hris-openapi.yaml
  format: yaml
  label: Unified.to HR & Directory API
  slug: hris-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-hris-openapi.yaml
- filename: unified-to-productivity-openapi.yaml
  format: yaml
  label: Unified.to Messaging API
  slug: messaging-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-productivity-openapi.yaml
- filename: unified-to-it-ops-openapi.yaml
  format: yaml
  label: Unified.to Payments API
  slug: payment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-it-ops-openapi.yaml
- filename: unified-to-it-ops-openapi.yaml
  format: yaml
  label: Unified.to Ticketing API
  slug: ticketing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/openapi/unified-to-it-ops-openapi.yaml
categories:
- components
- delete
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
description: Spectral linting rules defining API design standards and conventions for Unified.to.
layout: rules
name: Unified.to API Rules
provider_name: Unified.to
provider_slug: unified-to
rule_count: 34
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.info.title
  name: info-title-contains-unified
  severity: warn
- description: ''
  given: $.info
  name: info-description-required
  severity: warn
- description: ''
  given: $.info
  name: info-version-required
  severity: error
- description: ''
  given: $
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
  name: servers-unified-to-domain
  severity: info
- description: ''
  given: $.paths[*]~
  name: paths-connection-id-required
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: ''
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name=='connection_id')]
  name: parameter-connection-id-path
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*].get.parameters[?(@.name=='limit')]
  name: parameter-pagination-limit
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameter-snake-case
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: response-401-unauthorized
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch]
  name: response-422-validation
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: warn
- description: ''
  given: $.components.schemas[?(@.type=='object')]
  name: schema-raw-property-present
  severity: info
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: error
- description: ''
  given: $.components.securitySchemes[*][?(@.type=='http')]
  name: security-jwt-bearer
  severity: warn
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: ''
  given: $.paths[*].delete.responses
  name: delete-returns-200-or-204
  severity: info
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.components
  name: components-schemas-defined
  severity: error
- description: ''
  given: $.components.schemas[?(!@.title)]
  name: schema-raw-passthrough
  severity: info
rules_file: rules/unified-to-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/rules/unified-to-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 7
  warn: 14
slug: unified-to-spectral-rules
source_filename: unified-to-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # ─── INFO / METADATA ───────────────────────────────────────────────────────\n\n  info-title-required:\n    message: API info title is required\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-title-contains-unified:\n    message: API title should reference Unified.to\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)unified\"\n\n  info-description-required:\n    message: API info description is required\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: API info version is required\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # ─── OPENAPI VERSION ────────────────────────────────────────────────────────\n\n  openapi-version-3:\n    message: OpenAPI version must be 3.x\n    severity: error\n\
  \    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # ─── SERVERS ────────────────────────────────────────────────────────────────\n\n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-unified-to-domain:\n    message: Server should be on api.unified.to or regional subdomain\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"unified\\\\.to\"\n\n  # ─── PATHS — NAMING CONVENTIONS ─────────────────────────────────────────────\n\n  paths-connection-id-required:\n    message: API resource paths should include {connection_id}\
  \ parameter\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(unified|[a-z]+/\\\\{connection_id\\\\})\"\n\n  paths-kebab-case:\n    message: Path segments should use snake_case or kebab-case (Unified.to convention)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9_{}/-]+)+$\"\n\n  paths-no-trailing-slash:\n    message: Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # ─── OPERATIONS ─────────────────────────────────────────────────────────────\n\n  operation-id-required:\n    message: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-summary-required:\n   \
  \ message: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    message: Operation summaries should use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-tags-required:\n    message: Every operation should have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  operation-description-required:\n    message: Every operation should have a description\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  # ─── PARAMETERS ─────────────────────────────────────────────────────────────\n\
  \n  parameter-connection-id-path:\n    message: connection_id path parameter should be defined when present\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name=='connection_id')]\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values:\n          - path\n\n  parameter-description-required:\n    message: All parameters should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-pagination-limit:\n    message: List operations should support a limit parameter\n    severity: info\n    given: $.paths[*].get.parameters[?(@.name=='limit')]\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n          - number\n\n  parameter-snake-case:\n    message: Parameter names should use snake_case (Unified.to convention)\n   \
  \ severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # ─── REQUEST BODIES ──────────────────────────────────────────────────────────\n\n  request-body-json:\n    message: Request bodies should use application/json content type\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  # ─── RESPONSES ───────────────────────────────────────────────────────────────\n\n  response-success-defined:\n    message: Every operation must define at least one 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: truthy\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n\
  \    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  response-401-unauthorized:\n    message: Protected operations should define 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses.401\n      function: truthy\n\n  response-422-validation:\n    message: Write operations should define a 422 validation error response\n    severity: info\n    given: $.paths[*][post,put,patch]\n    then:\n      field: responses.422\n      function: truthy\n\n  # ─── SCHEMAS — PROPERTY NAMING ───────────────────────────────────────────────\n\n  schema-property-snake-case:\n    message: Schema properties should use snake_case (Unified.to convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  schema-raw-property-present:\n    message:\
  \ Domain model schemas should include a 'raw' property for provider-specific data\n    severity: info\n    given: $.components.schemas[?(@.type=='object')]\n    then:\n      field: properties.raw\n      function: truthy\n\n  # ─── SECURITY ────────────────────────────────────────────────────────────────\n\n  security-schemes-defined:\n    message: Security schemes must be defined\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-jwt-bearer:\n    message: Unified.to uses JWT bearer token authentication\n    severity: warn\n    given: $.components.securitySchemes[*][?(@.type=='http')]\n    then:\n      field: scheme\n      function: enumeration\n      functionOptions:\n        values:\n          - bearer\n\n  # ─── HTTP METHOD CONVENTIONS ─────────────────────────────────────────────────\n\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n\
  \    then:\n      field: requestBody\n      function: falsy\n\n  delete-returns-200-or-204:\n    message: DELETE operations should return 200 (with body) or 204 (no content)\n    severity: info\n    given: $.paths[*].delete.responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  # ─── GENERAL QUALITY ─────────────────────────────────────────────────────────\n\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  components-schemas-defined:\n    message: Components schemas section should be defined for reusable types\n    severity: error\n    given: $.components\n    then:\n      field: schemas\n      function: truthy\n\n  schema-raw-passthrough:\n    message: >-\n      Each domain model should have a 'raw' passthrough object for provider-specific\n\
  \      fields not covered by the unified schema.\n    severity: info\n    given: $.components.schemas[?(!@.title)]\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unified-to/refs/heads/main/rules/unified-to-spectral-rules.yml
tags:
- Integrations
- Unified API
- Spectral
- Linting
- API Governance
---
