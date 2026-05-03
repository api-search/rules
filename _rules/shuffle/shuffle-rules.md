---
api_specs:
- filename: shuffle-openapi.yml
  format: yaml
  label: Shuffle API
  slug: shuffle-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shuffle/refs/heads/main/openapi/shuffle-openapi.yml
categories:
- shuffle
description: Spectral linting rules defining API design standards and conventions for Shuffle.
layout: rules
name: Shuffle API Rules
provider_name: Shuffle
provider_slug: shuffle
rule_count: 9
rules:
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: shuffle-operation-tags
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: shuffle-operation-summary
  severity: error
- description: API must use Bearer token authentication
  given: $.components.securitySchemes[*]
  name: shuffle-bearer-auth
  severity: error
- description: Standard API responses should include success boolean
  given: $.components.schemas.ApiResponse
  name: shuffle-api-response
  severity: warn
- description: Workflow operations should use consistent id parameter naming
  given: $.paths['/workflows/{id}'][*].parameters[?(@.name == 'id')]
  name: shuffle-workflow-id
  severity: warn
- description: All operations must have a 200 response
  given: $.paths[*][*].responses
  name: shuffle-response-200
  severity: error
- description: Operations should document 401 Unauthorized response
  given: $.paths[*].get.responses
  name: shuffle-response-401
  severity: warn
- description: All operations must have an operationId in camelCase
  given: $.paths[*][*]
  name: shuffle-operation-id
  severity: error
- description: All API paths should use /api/v1 prefix (reflected in servers)
  given: $.servers[*]
  name: shuffle-v1-prefix
  severity: warn
rules_file: rules/shuffle-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shuffle/refs/heads/main/rules/shuffle-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: shuffle-rules
source_filename: shuffle-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shuffle-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  shuffle-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: summary\n      function: truthy\n\n  shuffle-bearer-auth:\n    description: API must use Bearer token authentication\n    message: \"Security scheme must be HTTP Bearer\"\n    given: \"$.components.securitySchemes[*]\"\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              enum: [http]\n            scheme:\n              enum: [bearer]\n\n  shuffle-api-response:\n    description: Standard API responses\
  \ should include success boolean\n    message: \"API response schemas should include success field\"\n    given: \"$.components.schemas.ApiResponse\"\n    severity: warn\n    then:\n      field: properties.success\n      function: truthy\n\n  shuffle-workflow-id:\n    description: Workflow operations should use consistent id parameter naming\n    message: \"Workflow path parameters should use 'id' for workflow identifier\"\n    given: \"$.paths['/workflows/{id}'][*].parameters[?(@.name == 'id')]\"\n    severity: warn\n    then:\n      field: required\n      function: truthy\n\n  shuffle-response-200:\n    description: All operations must have a 200 response\n    message: \"Operation must define a 200 response\"\n    given: \"$.paths[*][*].responses\"\n    severity: error\n    then:\n      field: \"200\"\n      function: truthy\n\n  shuffle-response-401:\n    description: Operations should document 401 Unauthorized response\n    message: \"Authenticated endpoints should document 401 response\"\
  \n    given: \"$.paths[*].get.responses\"\n    severity: warn\n    then:\n      field: \"401\"\n      function: defined\n\n  shuffle-operation-id:\n    description: All operations must have an operationId in camelCase\n    message: \"Operation must have an operationId\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  shuffle-v1-prefix:\n    description: All API paths should use /api/v1 prefix (reflected in servers)\n    message: \"API version should be specified in server URL\"\n    given: \"$.servers[*]\"\n    severity: warn\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https?://.*/(api/)?v[0-9]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shuffle/refs/heads/main/rules/shuffle-rules.yml
tags:
- Security
- Workflows
- Automation
- SOAR
- Orchestration
- Open Source
- Spectral
- Linting
- API Governance
---
