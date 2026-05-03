---
api_specs:
- filename: stackone-openapi.yml
  format: yaml
  label: StackOne
  slug: stackone
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stackone/refs/heads/main/openapi/stackone-openapi.yml
categories:
- stackone
description: Spectral linting rules defining API design standards and conventions for StackOne.
layout: rules
name: StackOne API Rules
provider_name: StackOne
provider_slug: stackone
rule_count: 7
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: stackone-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stackone-tags-required
  severity: error
- description: Unified API paths must start with /unified/{category}/
  given: $.paths[?(/unified/)][*]~
  name: stackone-unified-path-prefix
  severity: warn
- description: StackOne API server must be api.stackone.com
  given: $.servers[*].url
  name: stackone-v1-server
  severity: error
- description: Requests must use basic authentication
  given: $.components.securitySchemes
  name: stackone-bearer-auth
  severity: warn
- description: All operations must define at least one success response
  given: $.paths[*][*].responses
  name: stackone-successful-response
  severity: error
- description: Collection resource paths must use plural nouns
  given: $.paths[*]~
  name: stackone-plural-collection-paths
  severity: warn
rules_file: rules/stackone-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stackone/refs/heads/main/rules/stackone-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 3
slug: stackone-rules
source_filename: stackone-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  stackone-operation-ids:\n    description: All operations must have an operationId\n    message: 'Operation must have an operationId: {{path}}'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: operationId\n      function: truthy\n\n  stackone-tags-required:\n    description: All operations must have at least one tag\n    message: 'Operation at {{path}} must have at least one tag'\n    severity: error\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: truthy\n\n  stackone-unified-path-prefix:\n    description: Unified API paths must start with /unified/{category}/\n    message: 'Unified API path {{path}} must begin with /unified/'\n    severity: warn\n    given: '$.paths[?(/unified/)][*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/unified/'\n\n  stackone-v1-server:\n    description: StackOne API server must be api.stackone.com\n    message: 'Server URL must be https://api.stackone.com'\n\
  \    severity: error\n    given: '$.servers[*].url'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://api\\.stackone\\.com'\n\n  stackone-bearer-auth:\n    description: Requests must use basic authentication\n    message: 'Operation {{path}} should use basic or bearer auth'\n    severity: warn\n    given: '$.components.securitySchemes'\n    then:\n      function: truthy\n\n  stackone-successful-response:\n    description: All operations must define at least one success response\n    message: 'Operation at {{path}} must define a 200, 201, or 204 response'\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  stackone-plural-collection-paths:\n    description: Collection resource paths must use plural nouns\n    message: 'Collection path {{path}} should\
  \ use plural nouns'\n    severity: warn\n    given: '$.paths[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: '/unified/[^/]+/[a-z]+$(?<!s)'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stackone/refs/heads/main/rules/stackone-rules.yml
tags:
- Integrations
- iPaaS
- Spectral
- Linting
- API Governance
---
