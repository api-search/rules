---
api_specs:
- filename: unisys-stealth-ecoapi-openapi.yaml
  format: yaml
  label: Unisys Stealth EcoAPI
  slug: unisys-stealth-ecoapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unisys/refs/heads/main/openapi/unisys-stealth-ecoapi-openapi.yaml
categories:
- components
- get
- info
- isolation
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
- stealth
description: Spectral linting rules defining API design standards and conventions for Unisys.
layout: rules
name: Unisys API Rules
provider_name: Unisys
provider_slug: unisys
rule_count: 30
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.info.title
  name: info-title-contains-unisys
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
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: ''
  given: $.paths[*]~
  name: stealth-paths-use-api-prefix
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-id-camel-case
  severity: warn
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
  name: operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
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
  name: response-400-bad-request
  severity: info
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: error
- description: ''
  given: $.components.securitySchemes[*]
  name: security-basic-auth
  severity: warn
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: ''
  given: $.paths[?(@property =~ /isolate|unisolate/)][*]
  name: isolation-uses-post
  severity: info
- description: ''
  given: $.components.schemas[*].properties[*]~
  name: schema-property-camel-case
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: ''
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: ''
  given: $.components
  name: components-schemas-defined
  severity: error
rules_file: rules/unisys-stealth-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unisys/refs/heads/main/rules/unisys-stealth-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 3
  warn: 14
slug: unisys-stealth-spectral-rules
source_filename: unisys-stealth-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # ─── INFO / METADATA ───────────────────────────────────────────────────────\n\n  info-title-required:\n    message: API info title is required\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-title-contains-unisys:\n    message: API title should reference Unisys\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)unisys\"\n\n  info-description-required:\n    message: API info description is required\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    message: API info version is required\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # ─── OPENAPI VERSION ────────────────────────────────────────────────────────\n\n  openapi-version-3:\n    message: OpenAPI version must be 3.x\n    severity: error\n\
  \    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # ─── SERVERS ────────────────────────────────────────────────────────────────\n\n  servers-defined:\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    message: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # ─── PATHS — NAMING CONVENTIONS ─────────────────────────────────────────────\n\n  paths-no-trailing-slash:\n    message: Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  stealth-paths-use-api-prefix:\n    message: Unisys Stealth EcoAPI paths should begin with /api/\n    severity: info\n\
  \    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/\"\n\n  # ─── OPERATIONS ─────────────────────────────────────────────────────────────\n\n  operation-id-required:\n    message: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    message: operationId should use camelCase (Unisys convention)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-summary-required:\n    message: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    message: Operation summaries\
  \ should start with an uppercase letter\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-description-required:\n    message: Every operation should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    message: Every operation should have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # ─── PARAMETERS ─────────────────────────────────────────────────────────────\n\n  parameter-description-required:\n    message: All parameters should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\
  \n  parameter-schema-required:\n    message: All parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # ─── REQUEST BODIES ──────────────────────────────────────────────────────────\n\n  request-body-description:\n    message: Request bodies should have a description\n    severity: warn\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  # ─── RESPONSES ───────────────────────────────────────────────────────────────\n\n  response-success-defined:\n    message: Every operation must define at least one 2xx success response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: truthy\n\n  response-description-required:\n    message: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n\
  \    then:\n      field: description\n      function: truthy\n\n  response-401-unauthorized:\n    message: Protected operations should define 401 Unauthorized response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses.401\n      function: truthy\n\n  response-400-bad-request:\n    message: Write operations should define 400 Bad Request response\n    severity: info\n    given: $.paths[*][post,put,patch]\n    then:\n      field: responses.400\n      function: truthy\n\n  # ─── SECURITY ────────────────────────────────────────────────────────────────\n\n  security-schemes-defined:\n    message: Security schemes must be defined\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-basic-auth:\n    message: Unisys Stealth EcoAPI uses HTTP Basic Authentication\n    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      field: type\n      function:\
  \ enumeration\n      functionOptions:\n        values:\n          - http\n\n  # ─── HTTP METHOD CONVENTIONS ─────────────────────────────────────────────────\n\n  get-no-request-body:\n    message: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  isolation-uses-post:\n    message: >-\n      Isolation and un-isolation operations should use POST method\n    severity: info\n    given: $.paths[?(@property =~ /isolate|unisolate/)][*]\n    then:\n      function: truthy\n\n  # ─── SCHEMAS — PROPERTY NAMING ───────────────────────────────────────────────\n\n  schema-property-camel-case:\n    message: Schema properties should use camelCase (Unisys convention)\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-description-required:\n    message: Top-level component\
  \ schemas should have descriptions\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # ─── GENERAL QUALITY ─────────────────────────────────────────────────────────\n\n  no-empty-descriptions:\n    message: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  components-schemas-defined:\n    message: Components schemas section should be defined\n    severity: error\n    given: $.components\n    then:\n      field: schemas\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unisys/refs/heads/main/rules/unisys-stealth-spectral-rules.yml
tags:
- Security
- Zero Trust
- Network Security
- IT Services
- Cybersecurity
- Enterprise Technology
- Spectral
- Linting
- API Governance
---
