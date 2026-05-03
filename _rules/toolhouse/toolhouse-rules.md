---
api_specs:
- filename: toolhouse-openapi-original.yml
  format: yaml
  label: Toolhouse Platform API
  slug: platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toolhouse/refs/heads/main/openapi/toolhouse-openapi-original.yml
categories:
- toolhouse
description: Spectral linting rules defining API design standards and conventions for Toolhouse.
layout: rules
name: Toolhouse API Rules
provider_name: Toolhouse
provider_slug: toolhouse
rule_count: 10
rules:
- description: Operation summaries must use Title Case and start with "Toolhouse"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: toolhouse-operation-summary-title-case
  severity: warn
- description: OperationIds should be lowercase snake_case
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: toolhouse-operation-id-snake-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: toolhouse-operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: toolhouse-operation-summary-required
  severity: error
- description: API uses HTTPBearer authentication - security scheme should be defined
  given: $.components.securitySchemes
  name: toolhouse-security-bearer-auth
  severity: error
- description: User-scoped paths should follow /me/{resource} pattern
  given: $.paths
  name: toolhouse-me-path-structure
  severity: hint
- description: Path parameters ending in _id that use UUID values should have format uuid
  given: $.paths[*][*].parameters[?(@.in=='path')][?(@.name=~/_id$/)]
  name: toolhouse-uuid-path-param-format
  severity: warn
- description: POST/PUT/PATCH operations should document 422 Validation Error response
  given: $.paths[*][post,put,patch].responses
  name: toolhouse-validation-error-documented
  severity: warn
- description: Tags used on operations should be defined at the top level
  given: $
  name: toolhouse-tags-defined
  severity: warn
- description: Request bodies should be marked as required for POST/PUT/PATCH
  given: $.paths[*][post,put,patch].requestBody
  name: toolhouse-request-body-required
  severity: warn
rules_file: rules/toolhouse-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toolhouse/refs/heads/main/rules/toolhouse-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: toolhouse-rules
source_filename: toolhouse-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n  # Toolhouse API uses Title Case summaries with \"Toolhouse\" prefix\n  toolhouse-operation-summary-title-case:\n    description: Operation summaries must use Title Case and start with \"Toolhouse\"\n    message: \"Operation summary '{{value}}' should start with 'Toolhouse' and use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Toolhouse [A-Z]\"\n\n  # All operationIds should follow snake_case style (auto-generated FastAPI pattern)\n  toolhouse-operation-id-snake-case:\n    description: OperationIds should be lowercase snake_case\n    message: \"OperationId '{{value}}' should be snake_case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]+$\"\n\n  # All operations must have operationId\n\
  \  toolhouse-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # All operations must have a summary\n  toolhouse-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Bearer token authentication must be defined consistently\n  toolhouse-security-bearer-auth:\n    description: API uses HTTPBearer authentication - security scheme should be defined\n    message: \"Security scheme HTTPBearer must be defined in components.securitySchemes\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: HTTPBearer\n      function: truthy\n\
  \n  # Paths under /me/ are user-scoped - should follow /me/{resource} pattern\n  toolhouse-me-path-structure:\n    description: User-scoped paths should follow /me/{resource} pattern\n    message: \"Path '{{value}}' under /me/ should follow /me/{resource} convention\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/me/[a-z]\"\n\n  # UUIDs used as path parameters should be typed as uuid format\n  toolhouse-uuid-path-param-format:\n    description: Path parameters ending in _id that use UUID values should have format uuid\n    message: \"Path parameter '{{path}}' appears to be a UUID but may be missing format: uuid\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')][?(@.name=~/_id$/)]\"\n    then:\n      field: schema.format\n      function: truthy\n\n  # Responses should document 422 Validation Error for POST/PUT/PATCH\n  toolhouse-validation-error-documented:\n    description: POST/PUT/PATCH\
  \ operations should document 422 Validation Error response\n    message: \"Operation is missing 422 Validation Error response\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].responses\"\n    then:\n      field: \"422\"\n      function: truthy\n\n  # Tags should be defined globally when used on operations\n  toolhouse-tags-defined:\n    description: Tags used on operations should be defined at the top level\n    message: \"Top-level tags array should be defined\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\n  # Request bodies for POST/PUT/PATCH must be marked required\n  toolhouse-request-body-required:\n    description: Request bodies should be marked as required for POST/PUT/PATCH\n    message: \"Request body should be marked as required\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toolhouse/refs/heads/main/rules/toolhouse-rules.yml
tags:
- Agent Infrastructure
- AI Agents
- Backend as a Service
- MCP
- Tools
- Spectral
- Linting
- API Governance
---
