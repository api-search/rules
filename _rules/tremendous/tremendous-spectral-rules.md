---
api_specs:
- filename: tremendous-api-openapi.yml
  format: yaml
  label: Tremendous API
  slug: tremendous
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tremendous/refs/heads/main/openapi/tremendous-api-openapi.yml
categories:
- tremendous
description: Spectral linting rules defining API design standards and conventions for Tremendous.
layout: rules
name: Tremendous API Rules
provider_name: Tremendous
provider_slug: tremendous
rule_count: 12
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tremendous-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tremendous-summary-title-case
  severity: warn
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: tremendous-security-defined
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: tremendous-response-200-get
  severity: error
- description: Authenticated operations should define a 401 response
  given: $.paths[*][get,post,put,patch,delete]
  name: tremendous-response-401-defined
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: tremendous-tag-defined
  severity: warn
- description: Tremendous API uses Bearer token (API key) authentication
  given: $.components.securitySchemes.BearerAuth
  name: tremendous-bearer-auth
  severity: info
- description: Path parameters use snake_case
  given: $.paths[*]~
  name: tremendous-path-snake-case
  severity: warn
- description: POST operations should define a request body
  given: $.paths[*].post
  name: tremendous-post-request-body
  severity: warn
- description: Tremendous API enforces rate limits - 429 should be documented
  given: $.paths[*][get,post]
  name: tremendous-rate-limit-response
  severity: info
- description: Create operations should document external_id for idempotency
  given: $.paths['/orders'].post.requestBody.content.application/json.schema
  name: tremendous-idempotency-external-id
  severity: info
- description: List operations should support pagination with offset and limit
  given: $.paths[*].get
  name: tremendous-list-pagination
  severity: info
rules_file: rules/tremendous-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tremendous/refs/heads/main/rules/tremendous-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 6
slug: tremendous-spectral-rules
source_filename: tremendous-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  tremendous-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tremendous-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /()+&-]*$\"\n\n  tremendous-security-defined:\n    description: All operations must define security requirements\n    message: \"Operation must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  tremendous-response-200-get:\n    description:\
  \ All GET operations must define a 200 response\n    message: \"GET operation must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  tremendous-response-401-defined:\n    description: Authenticated operations should define a 401 response\n    message: \"Operation should define 401 Unauthorized\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: defined\n\n  tremendous-tag-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  tremendous-bearer-auth:\n    description: Tremendous API uses Bearer token (API key) authentication\n    message: \"Use BearerAuth security scheme\"\n    severity: info\n    given:\
  \ \"$.components.securitySchemes.BearerAuth\"\n    then:\n      function: defined\n\n  tremendous-path-snake-case:\n    description: Path parameters use snake_case\n    message: \"Path segments should use snake_case or kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9_-]*(/[a-z][a-z0-9_-]*|/\\\\{[a-zA-Z][a-zA-Z0-9_]*\\\\})*)+$\"\n\n  tremendous-post-request-body:\n    description: POST operations should define a request body\n    message: \"POST operation should include a requestBody\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  tremendous-rate-limit-response:\n    description: Tremendous API enforces rate limits - 429 should be documented\n    message: \"Operation should define 429 Too Many Requests response\"\n    severity: info\n    given: \"$.paths[*][get,post]\"\n    then:\n      field: responses.429\n \
  \     function: defined\n\n  tremendous-idempotency-external-id:\n    description: Create operations should document external_id for idempotency\n    message: \"Order creation supports external_id for idempotent requests\"\n    severity: info\n    given: \"$.paths['/orders'].post.requestBody.content.application/json.schema\"\n    then:\n      function: defined\n\n  tremendous-list-pagination:\n    description: List operations should support pagination with offset and limit\n    message: \"List endpoint should support offset and limit parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tremendous/refs/heads/main/rules/tremendous-spectral-rules.yml
tags:
- Employee Incentives
- Global Payouts
- Incentives
- Market Research
- Payouts
- Rewards
- Spectral
- Linting
- API Governance
---
