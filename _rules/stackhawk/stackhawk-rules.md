---
api_specs:
- filename: stackhawk-openapi.json
  format: json
  label: StackHawk API
  slug: stackhawk-api
  spec_type: OpenAPI
  url: https://download.stackhawk.com/openapi/stackhawk-openapi.json
categories:
- stackhawk
description: Spectral linting rules defining API design standards and conventions for StackHawk.
layout: rules
name: StackHawk API Rules
provider_name: StackHawk
provider_slug: stackhawk
rule_count: 7
rules:
- description: All operations must have a camelCase operationId
  given: $.paths[*][*]
  name: stackhawk-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stackhawk-tags-required
  severity: error
- description: All StackHawk API paths should begin with /api/v1/ or /api/v2/
  given: $.paths[*]~
  name: stackhawk-api-versioned-path
  severity: warn
- description: Non-login operations must use BearerAuth
  given: $.paths[*][*]
  name: stackhawk-bearer-auth
  severity: warn
- description: Organization-scoped endpoints must use orgId path parameter
  given: $.paths['/api/v1/org/{orgId}'][*].parameters[?(@.in=='path')]
  name: stackhawk-org-id-param
  severity: warn
- description: All operations must define at least one success response
  given: $.paths[*][*].responses
  name: stackhawk-successful-response
  severity: error
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: stackhawk-delete-returns-204
  severity: warn
rules_file: rules/stackhawk-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stackhawk/refs/heads/main/rules/stackhawk-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: stackhawk-rules
source_filename: stackhawk-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  stackhawk-operation-ids:\n    description: All operations must have a camelCase operationId\n    message: 'Operation must have a camelCase operationId: {{path}}'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: operationId\n      function: truthy\n\n  stackhawk-tags-required:\n    description: All operations must have at least one tag\n    message: 'Operation at {{path}} must have at least one tag'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: truthy\n\n  stackhawk-api-versioned-path:\n    description: All StackHawk API paths should begin with /api/v1/ or /api/v2/\n    message: 'Path {{path}} must begin with /api/v1/ or /api/v2/'\n    severity: warn\n    given: '$.paths[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/api/v[12]/'\n\n  stackhawk-bearer-auth:\n    description: Non-login operations must use BearerAuth\n    message: 'Operation at {{path}} must\
  \ use BearerAuth security scheme'\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: security\n      function: truthy\n\n  stackhawk-org-id-param:\n    description: Organization-scoped endpoints must use orgId path parameter\n    message: 'Organization endpoint should use orgId parameter name'\n    severity: warn\n    given: \"$.paths['/api/v1/org/{orgId}'][*].parameters[?(@.in=='path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            name:\n              pattern: '^orgId$'\n\n  stackhawk-successful-response:\n    description: All operations must define at least one success response\n    message: 'Operation at {{path}} must define a 200, 201, 202, or 204 response'\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required:\
  \ ['202']\n            - required: ['204']\n\n  stackhawk-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: 'DELETE operation at {{path}} should return 204'\n    severity: warn\n    given: '$.paths[*].delete.responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['204']\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stackhawk/refs/heads/main/rules/stackhawk-rules.yml
tags:
- API Security
- Application Security
- DAST
- Security Testing
- Vulnerability Management
- Spectral
- Linting
- API Governance
---
