---
api_specs:
- filename: stackrox-openapi.yml
  format: yaml
  label: StackRox API
  slug: stackrox-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stackrox/refs/heads/main/openapi/stackrox-openapi.yml
categories:
- stackrox
description: Spectral linting rules defining API design standards and conventions for StackRox.
layout: rules
name: StackRox API Rules
provider_name: StackRox
provider_slug: stackrox
rule_count: 6
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: stackrox-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stackrox-tags-required
  severity: error
- description: All StackRox API paths should begin with /v1/
  given: $.paths[*]~
  name: stackrox-v1-api-path
  severity: warn
- description: StackRox API should use ApiToken security scheme
  given: $.components.securitySchemes
  name: stackrox-api-token-auth
  severity: error
- description: All operations must define at least one success response
  given: $.paths[*][*].responses
  name: stackrox-successful-response
  severity: error
- description: Count endpoints should follow the {resource}count naming convention
  given: $.paths[?(/count/)][*]~
  name: stackrox-count-endpoint-naming
  severity: info
rules_file: rules/stackrox-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stackrox/refs/heads/main/rules/stackrox-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 1
slug: stackrox-rules
source_filename: stackrox-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  stackrox-operation-ids:\n    description: All operations must have an operationId\n    message: 'Operation must have an operationId: {{path}}'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: operationId\n      function: truthy\n\n  stackrox-tags-required:\n    description: All operations must have at least one tag\n    message: 'Operation at {{path}} must have at least one tag'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: truthy\n\n  stackrox-v1-api-path:\n    description: All StackRox API paths should begin with /v1/\n    message: 'Path {{path}} must begin with /v1/'\n    severity: warn\n    given: '$.paths[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/v1/'\n\n  stackrox-api-token-auth:\n    description: StackRox API should use ApiToken security scheme\n    message: 'Security scheme must include ApiToken'\n    severity: error\n    given: '$.components.securitySchemes'\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['ApiToken']\n\n  stackrox-successful-response:\n    description: All operations must define at least one success response\n    message: 'Operation at {{path}} must define a 200, 201, or 204 response'\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  stackrox-count-endpoint-naming:\n    description: Count endpoints should follow the {resource}count naming convention\n    message: 'Count endpoint {{path}} should follow /v1/{resource}count pattern'\n    severity: info\n    given: '$.paths[?(/count/)][*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: 'count$'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stackrox/refs/heads/main/rules/stackrox-rules.yml
tags:
- Compliance
- Container Security
- Kubernetes
- Open Source
- Runtime Protection
- Security
- Spectral
- Linting
- API Governance
---
