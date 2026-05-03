---
api_specs:
- filename: wells-fargo-gateway-api-openapi.yml
  format: yaml
  label: Wells Fargo Gateway API
  slug: gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wells-fargo/refs/heads/main/openapi/wells-fargo-gateway-api-openapi.yml
- filename: wells-fargo-account-transactions-api-openapi.yml
  format: yaml
  label: Wells Fargo Account Transactions API
  slug: account-transactions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wells-fargo/refs/heads/main/openapi/wells-fargo-account-transactions-api-openapi.yml
- filename: wells-fargo-ach-payments-api-openapi.yml
  format: yaml
  label: Wells Fargo ACH Payments API
  slug: ach-payments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wells-fargo/refs/heads/main/openapi/wells-fargo-ach-payments-api-openapi.yml
categories:
- api
- oauth2
- operation
- pagination
- path
- query
- response
description: Spectral linting rules defining API design standards and conventions for wells-fargo.
layout: rules
name: wells-fargo API Rules
provider_name: wells-fargo
provider_slug: wells-fargo
rule_count: 12
rules:
- description: All Wells Fargo API paths must include a version segment (/v1/, /v2/, /v3/).
  given: $.paths[*]~
  name: api-versioned-paths
  severity: warn
- description: APIs must use OAuth 2.0 security scheme.
  given: $.components.securitySchemes[*]
  name: oauth2-security-scheme
  severity: error
- description: All operations must declare security requirements with scopes.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-security-scopes
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Operation IDs must use lowerCamelCase naming.
  given: $.paths[*][*].operationId
  name: operation-id-camel-case
  severity: warn
- description: Path parameter names should use lowerCamelCase.
  given: $.paths[*][*].parameters[?(@.in=='path')].name
  name: path-params-camel-case
  severity: warn
- description: Query parameter names should use lowerCamelCase.
  given: $.paths[*][*].parameters[?(@.in=='query')].name
  name: query-params-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: operation-summary-title-case
  severity: warn
- description: Operations with security must define a 401 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-defined
  severity: warn
- description: POST and PUT operations must define a 400 response for validation errors.
  given: $.paths[*][post,put].responses
  name: response-400-on-write
  severity: warn
- description: Paginated GET endpoints should use pageSize and pageToken parameters.
  given: $.paths[*].get.parameters[*].name
  name: pagination-page-size-param
  severity: hint
rules_file: rules/wells-fargo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wells-fargo/refs/heads/main/rules/wells-fargo-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 7
slug: wells-fargo-rules
source_filename: wells-fargo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # API versioning conventions\n  api-versioned-paths:\n    description: All Wells Fargo API paths must include a version segment (/v1/, /v2/, /v3/).\n    message: \"Path '{{property}}' must include a version prefix (e.g., /v2/, /v3/).\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  # OAuth 2.0 required\n  oauth2-security-scheme:\n    description: APIs must use OAuth 2.0 security scheme.\n    message: \"Security scheme must use OAuth 2.0 client credentials flow.\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values: [oauth2]\n\n  # Scoped security on all operations\n  operation-security-scopes:\n    description: All operations must declare security requirements with scopes.\n    message: \"Operation '{{path}}' must define OAuth 2.0 security\
  \ scopes.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # Operation IDs required\n  operation-id-required:\n    description: All operations must have an operationId.\n    message: \"Operation at '{{path}}' must define an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # Operation IDs must be lowerCamelCase\n  operation-id-camel-case:\n    description: Operation IDs must use lowerCamelCase naming.\n    message: \"OperationId '{{value}}' must use lowerCamelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Path parameters use lowerCamelCase\n  path-params-camel-case:\n    description: Path parameter names should use lowerCamelCase.\n    message: \"Path parameter '{{value}}'\
  \ should use lowerCamelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Query parameters use lowerCamelCase\n  query-params-camel-case:\n    description: Query parameter names should use lowerCamelCase.\n    message: \"Query parameter '{{value}}' should use lowerCamelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z_][a-zA-Z0-9_]*$\"\n\n  # Summaries required\n  operation-summary-required:\n    description: All operations must have a summary.\n    message: \"Operation at '{{path}}' must have a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Summaries must use Title Case\n  operation-summary-title-case:\n    description:\
  \ Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # 401 response defined on secured operations\n  response-401-defined:\n    description: Operations with security must define a 401 response.\n    message: \"Secured operation at '{{path}}' must define 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  # 400 response on POST/PUT operations\n  response-400-on-write:\n    description: POST and PUT operations must define a 400 response for validation errors.\n    message: \"Write operation at '{{path}}' must define a 400 Bad Request response.\"\n    severity: warn\n    given: \"$.paths[*][post,put].responses\"\n    then:\n      field: \"400\"\n      function: defined\n\
  \n  # Pagination parameters standardized\n  pagination-page-size-param:\n    description: Paginated GET endpoints should use pageSize and pageToken parameters.\n    message: \"Paginated endpoint should use 'pageSize' and 'pageToken' as pagination parameters.\"\n    severity: hint\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(pageSize|pageToken|startDate|endDate|[a-z][a-zA-Z0-9]*)$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wells-fargo/refs/heads/main/rules/wells-fargo-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
