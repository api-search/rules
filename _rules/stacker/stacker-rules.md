---
api_specs:
- filename: stacker-openapi.yml
  format: yaml
  label: Stacker API
  slug: stacker-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stacker/refs/heads/main/openapi/stacker-openapi.yml
categories:
- stacker
description: Spectral linting rules defining API design standards and conventions for Stacker.
layout: rules
name: Stacker API Rules
provider_name: Stacker
provider_slug: stacker
rule_count: 7
rules:
- description: All operations must have an operationId in camelCase
  given: $.paths[*][*]
  name: stacker-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stacker-tags-required
  severity: error
- description: All Stacker API paths end with a trailing slash
  given: $.paths[*]~
  name: stacker-trailing-slash
  severity: warn
- description: Operations must use IntegrationKey security scheme
  given: $.paths[*][*]
  name: stacker-header-auth
  severity: warn
- description: All operations must have a 200 or 201 success response
  given: $.paths[*][*].responses
  name: stacker-response-200-or-201
  severity: error
- description: Paths using object SID must name the parameter object_sid
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: stacker-object-sid-path-param
  severity: warn
- description: Request bodies must use application/json
  given: $.paths[*][*].requestBody.content
  name: stacker-content-type-json
  severity: warn
rules_file: rules/stacker-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stacker/refs/heads/main/rules/stacker-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: stacker-rules
source_filename: stacker-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  stacker-operation-ids:\n    description: All operations must have an operationId in camelCase\n    message: 'Operation must have a camelCase operationId: {{path}}'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: operationId\n      function: truthy\n\n  stacker-tags-required:\n    description: All operations must have at least one tag\n    message: 'Operation at {{path}} must have at least one tag'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: truthy\n\n  stacker-trailing-slash:\n    description: All Stacker API paths end with a trailing slash\n    message: 'Stacker API path {{path}} must end with a trailing slash'\n    severity: warn\n    given: '$.paths[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '/$'\n\n  stacker-header-auth:\n    description: Operations must use IntegrationKey security scheme\n    message: 'Operation at {{path}} must declare security\
  \ with IntegrationKey'\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: security\n      function: truthy\n\n  stacker-response-200-or-201:\n    description: All operations must have a 200 or 201 success response\n    message: 'Operation at {{path}} must define a 200 or 201 response'\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  stacker-object-sid-path-param:\n    description: Paths using object SID must name the parameter object_sid\n    message: 'Object SID path parameter should be named object_sid'\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              description:\n                pattern: object\n  \
  \        then:\n            properties:\n              name:\n                pattern: '^object_sid$'\n\n  stacker-content-type-json:\n    description: Request bodies must use application/json\n    message: 'Request body at {{path}} should use application/json content type'\n    severity: warn\n    given: '$.paths[*][*].requestBody.content'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['application/json']\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stacker/refs/heads/main/rules/stacker-rules.yml
tags:
- Application Development
- Low-Code
- No-Code
- Portals
- Workflow Automation
- Spectral
- Linting
- API Governance
---
