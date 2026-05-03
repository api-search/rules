---
api_specs:
- filename: scispot-openapi.yml
  format: yaml
  label: Scispot API
  slug: scispot-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scispot/refs/heads/main/openapi/scispot-openapi.yml
categories:
- scispot
description: Spectral linting rules defining API design standards and conventions for Scispot.
layout: rules
name: Scispot API Rules
provider_name: Scispot
provider_slug: scispot
rule_count: 13
rules:
- description: Scispot API must use API key authentication via apiKey header
  given: $.components.securitySchemes.*.type
  name: scispot-apikey-auth-defined
  severity: error
- description: Operation IDs must use camelCase naming convention
  given: $.paths.*.*.operationId
  name: scispot-operation-id-camel-case
  severity: warn
- description: API paths must use kebab-case segments
  given: $.paths[*]~
  name: scispot-path-kebab-case
  severity: warn
- description: POST endpoints that create resources must return 201 Created
  given: $.paths.*.post.responses
  name: scispot-post-returns-201
  severity: warn
- description: DELETE endpoints must return 204 No Content on success
  given: $.paths.*.delete.responses
  name: scispot-delete-returns-204
  severity: warn
- description: All authenticated endpoints must define a 401 Unauthorized response
  given: $.paths.*.*.responses
  name: scispot-auth-401-response
  severity: warn
- description: Single-resource retrieval endpoints must define 404 response
  given: $.paths[*][?(@property == 'get')].responses
  name: scispot-single-resource-404
  severity: warn
- description: POST and PUT endpoints must define a request body
  given: $.paths.*[post,put]
  name: scispot-post-put-require-body
  severity: error
- description: All operations must have a description
  given: $.paths.*.*
  name: scispot-operation-description
  severity: warn
- description: All operations must be tagged
  given: $.paths.*.*
  name: scispot-operation-tags
  severity: warn
- description: List endpoints should support page and limit pagination parameters
  given: $.paths.*.get.parameters[*].name
  name: scispot-list-pagination-params
  severity: info
- description: Server URL must include API version prefix
  given: $.servers[*].url
  name: scispot-server-versioned
  severity: warn
- description: Response bodies should reference component schemas rather than inline definitions
  given: $.paths.*.*.responses.*.content.*.schema
  name: scispot-use-component-schemas
  severity: info
rules_file: rules/scispot-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scispot/refs/heads/main/rules/scispot-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 9
slug: scispot-rules
source_filename: scispot-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Scispot API Conventions\n\n  # Enforce API key authentication is defined\n  scispot-apikey-auth-defined:\n    description: Scispot API must use API key authentication via apiKey header\n    message: Security scheme must define apiKey authentication in the header\n    severity: error\n    given: $.components.securitySchemes.*.type\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - apiKey\n\n  # Enforce operation IDs use camelCase\n  scispot-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: Operation ID {{value}} must use camelCase\n    severity: warn\n    given: $.paths.*.*.operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Enforce paths use kebab-case\n  scispot-path-kebab-case:\n    description: API paths must use kebab-case segments\n    message: Path must use kebab-case\n\
  \    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9-{}]+)+$\"\n\n  # Enforce CRUD endpoints return 201 for creation\n  scispot-post-returns-201:\n    description: POST endpoints that create resources must return 201 Created\n    message: POST endpoint at {{path}} must include a 201 response for successful creation\n    severity: warn\n    given: $.paths.*.post.responses\n    then:\n      field: \"201\"\n      function: defined\n\n  # Enforce DELETE returns 204 No Content\n  scispot-delete-returns-204:\n    description: DELETE endpoints must return 204 No Content on success\n    message: DELETE endpoint at {{path}} must include a 204 response\n    severity: warn\n    given: $.paths.*.delete.responses\n    then:\n      field: \"204\"\n      function: defined\n\n  # Enforce 401 response on authenticated endpoints\n  scispot-auth-401-response:\n    description: All authenticated endpoints must define a 401\
  \ Unauthorized response\n    message: Endpoint at {{path}} must include a 401 response for authentication failures\n    severity: warn\n    given: $.paths.*.*.responses\n    then:\n      field: \"401\"\n      function: defined\n\n  # Enforce 404 response for single-resource GET endpoints\n  scispot-single-resource-404:\n    description: Single-resource retrieval endpoints must define 404 response\n    message: Single-resource GET at {{path}} must include a 404 response\n    severity: warn\n    given: $.paths[*][?(@property == 'get')].responses\n    then:\n      field: \"404\"\n      function: defined\n\n  # Enforce request body for POST and PUT\n  scispot-post-put-require-body:\n    description: POST and PUT endpoints must define a request body\n    message: POST/PUT endpoint at {{path}} must include a requestBody\n    severity: error\n    given: $.paths.*[post,put]\n    then:\n      field: requestBody\n      function: truthy\n\n  # Require descriptions on all operations\n  scispot-operation-description:\n\
  \    description: All operations must have a description\n    message: Operation at {{path}} must have a description\n    severity: warn\n    given: $.paths.*.*\n    then:\n      field: description\n      function: truthy\n\n  # Require tags on all operations\n  scispot-operation-tags:\n    description: All operations must be tagged\n    message: Operation at {{path}} must include at least one tag\n    severity: warn\n    given: $.paths.*.*\n    then:\n      field: tags\n      function: truthy\n\n  # Enforce pagination parameters on list endpoints\n  scispot-list-pagination-params:\n    description: List endpoints should support page and limit pagination parameters\n    message: List endpoint should support page and limit query parameters\n    severity: info\n    given: $.paths.*.get.parameters[*].name\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - limit\n          - type\n          - barcode\n          - sampleId\n     \
  \     - notebookId\n          - labsheetId\n\n  # Enforce version prefix in server URL\n  scispot-server-versioned:\n    description: Server URL must include API version prefix\n    message: Server URL must include version prefix (e.g., /v1)\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\/v[0-9]+$\"\n\n  # Enforce component schemas are reused\n  scispot-use-component-schemas:\n    description: Response bodies should reference component schemas rather than inline definitions\n    message: Use $ref to component schemas for consistency\n    severity: info\n    given: $.paths.*.*.responses.*.content.*.schema\n    then:\n      field: \"$ref\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scispot/refs/heads/main/rules/scispot-rules.yml
tags:
- Laboratory
- Life Science
- LIMS
- ELN
- Biotech
- API First
- Scientific Data
- Healthcare
- Spectral
- Linting
- API Governance
---
