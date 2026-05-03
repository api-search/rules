---
api_specs:
- filename: sandbox-banking-glyue-openapi.yml
  format: yaml
  label: Glyue Integration Gateway API
  slug: glyue
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sandbox-banking/refs/heads/main/openapi/sandbox-banking-glyue-openapi.yml
categories:
- sandbox
description: Spectral linting rules defining API design standards and conventions for Sandbox Banking.
layout: rules
name: Sandbox Banking API Rules
provider_name: Sandbox Banking
provider_slug: sandbox-banking
rule_count: 13
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sandbox-banking-operation-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: sandbox-banking-operation-id-camel-case
  severity: warn
- description: API path segments must use kebab-case.
  given: $.paths
  name: sandbox-banking-path-kebab-case
  severity: warn
- description: Glyue API uses token-based authentication via Authorization header.
  given: $.components.securitySchemes
  name: sandbox-banking-token-auth
  severity: error
- description: All 200 responses must include a content schema.
  given: $.paths[*][get,post,put].responses['200']
  name: sandbox-banking-response-200-schema
  severity: warn
- description: List endpoints must support pagination parameters (page and page_size).
  given: $.paths[?(!@property.match(/\{.*\}/))][get].parameters[*].name
  name: sandbox-banking-list-endpoint-pagination
  severity: info
- description: API paths must not end with a trailing slash.
  given: $.paths
  name: sandbox-banking-no-trailing-slash
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: sandbox-banking-tags-required
  severity: warn
- description: All operations must include a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: sandbox-banking-description-required
  severity: warn
- description: All API operations must declare a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sandbox-banking-401-defined
  severity: warn
- description: DELETE operations must not include a request body.
  given: $.paths[*][delete]
  name: sandbox-banking-delete-no-body
  severity: error
- description: Integration execution endpoints must use /run suffix.
  given: $.paths
  name: sandbox-banking-run-endpoint-naming
  severity: info
- description: API must expose run-history endpoint for regulatory compliance.
  given: $.paths
  name: sandbox-banking-audit-trail
  severity: error
rules_file: rules/sandbox-banking-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sandbox-banking/refs/heads/main/rules/sandbox-banking-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 7
slug: sandbox-banking-rules
source_filename: sandbox-banking-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # Sandbox Banking / Glyue Integration Gateway API conventions\n\n  sandbox-banking-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case (capitalize each word).\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  sandbox-banking-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sandbox-banking-path-kebab-case:\n    description: API path segments must use kebab-case.\n    message: \"Path segment must use kebab-case (lowercase with hyphens).\"\n\
  \    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z0-9-]+|\\\\{[a-zA-Z][a-zA-Z0-9_]*\\\\}))*$\"\n\n  sandbox-banking-token-auth:\n    description: Glyue API uses token-based authentication via Authorization header.\n    message: \"API must declare TokenAuth security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: TokenAuth\n      function: truthy\n\n  sandbox-banking-response-200-schema:\n    description: All 200 responses must include a content schema.\n    message: \"Operation '{{path}}' 200 response should include a content schema.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put].responses['200']\"\n    then:\n      field: content\n      function: truthy\n\n  sandbox-banking-list-endpoint-pagination:\n    description: List endpoints must support pagination parameters (page and page_size).\n    message: \"GET list endpoint '{{path}}' should\
  \ support page and page_size query parameters.\"\n    severity: info\n    given: \"$.paths[?(!@property.match(/\\\\{.*\\\\}/))][get].parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - page_size\n          - status\n          - start_date\n          - end_date\n          - integration_id\n\n  sandbox-banking-no-trailing-slash:\n    description: API paths must not end with a trailing slash.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  sandbox-banking-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation '{{path}}' must declare at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: array\n          minItems: 1\n\n  sandbox-banking-description-required:\n    description: All operations must include a description.\n    message: \"Operation '{{path}}' must include a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  sandbox-banking-401-defined:\n    description: All API operations must declare a 401 Unauthorized response.\n    message: \"Operation '{{path}}' must define a 401 response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  sandbox-banking-delete-no-body:\n    description: DELETE operations must not include a request body.\n    message: \"DELETE operation '{{path}}' must not have a request body.\"\n    severity: error\n    given: \"$.paths[*][delete]\"\n    then:\n      field: requestBody\n      function: falsy\n\n  sandbox-banking-run-endpoint-naming:\n\
  \    description: Integration execution endpoints must use /run suffix.\n    message: \"Integration run endpoint should use '{integrationId}/run' naming pattern.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*(\\\\/run|\\\\/execute|\\\\/trigger).*|.*integrations.*\"\n\n  sandbox-banking-audit-trail:\n    description: API must expose run-history endpoint for regulatory compliance.\n    message: \"Glyue API must include run-history endpoints for GLBA/FFIEC audit compliance.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*run-history.*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sandbox-banking/refs/heads/main/rules/sandbox-banking-rules.yml
tags:
- API Integration
- Banking
- Core Banking
- Credit Unions
- Financial Services
- Fintech
- Integration Platform
- iPaaS
- Open Banking
- Spectral
- Linting
- API Governance
---
