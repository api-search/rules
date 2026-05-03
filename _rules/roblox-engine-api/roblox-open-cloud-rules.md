---
api_specs:
- filename: openapi
  format: yaml
  label: Roblox Open Cloud API
  slug: roblox-open-cloud-api
  spec_type: OpenAPI
  url: https://create.roblox.com/docs/cloud/reference/openapi
categories:
- roblox
description: Spectral linting rules defining API design standards and conventions for Roblox Engine API.
layout: rules
name: Roblox Engine API API Rules
provider_name: Roblox Engine API
provider_slug: roblox-engine-api
rule_count: 11
rules:
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: roblox-operation-has-tag
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: roblox-operation-has-summary
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: roblox-operation-has-operation-id
  severity: error
- description: Roblox Open Cloud uses x-api-key header authentication
  given: $.components.securitySchemes[*]
  name: roblox-api-key-auth
  severity: warn
- description: Open Cloud v2 paths should use /cloud/v2/ prefix
  given: $.paths[*]~
  name: roblox-versioned-cloud-paths
  severity: info
- description: Universe endpoints should use universeId as path parameter
  given: $.paths[*][*].parameters[?(@.in === 'path' && @.name === 'universe_id')]
  name: roblox-universe-id-path-param
  severity: warn
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: roblox-camel-case-operation-id
  severity: warn
- description: Cloud v2 list endpoints should use pageToken for pagination
  given: $.paths[*].get.parameters[?(@.name === 'pageToken')]
  name: roblox-pagination-uses-page-token
  severity: info
- description: Error responses should reference an error schema
  given: $.paths[*][*].responses[4*].content[*]
  name: roblox-responses-have-error-schema
  severity: warn
- description: PATCH operations should support updateMask query parameter
  given: $.paths[*].patch
  name: roblox-patch-uses-update-mask
  severity: info
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: roblox-schema-has-description
  severity: info
rules_file: rules/roblox-open-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/roblox-engine-api/refs/heads/main/rules/roblox-open-cloud-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 5
slug: roblox-open-cloud-rules
source_filename: roblox-open-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Roblox Open Cloud API Conventions\n\n  roblox-operation-has-tag:\n    description: All operations must have at least one tag\n    message: Operation {{path}} is missing a tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  roblox-operation-has-summary:\n    description: All operations must have a summary\n    message: Operation {{path}} is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  roblox-operation-has-operation-id:\n    description: All operations must have an operationId\n    message: Operation {{path}} is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  roblox-api-key-auth:\n    description: Roblox Open Cloud uses x-api-key header\
  \ authentication\n    message: Security scheme should use apiKey with x-api-key header\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - apiKey\n            in:\n              type: string\n              enum:\n                - header\n            name:\n              type: string\n              enum:\n                - x-api-key\n\n  roblox-versioned-cloud-paths:\n    description: Open Cloud v2 paths should use /cloud/v2/ prefix\n    message: Cloud API path {{path}} should use /cloud/v2/ prefix\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(cloud|datastores|messaging-service|assets|universes)/\"\n\n  roblox-universe-id-path-param:\n    description: Universe endpoints should use universeId\
  \ as path parameter\n    message: Universe ID path parameter should be named universeId\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in === 'path' && @.name === 'universe_id')]\"\n    then:\n      function: falsy\n\n  roblox-camel-case-operation-id:\n    description: OperationIds should use camelCase\n    message: OperationId {{value}} should use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  roblox-pagination-uses-page-token:\n    description: Cloud v2 list endpoints should use pageToken for pagination\n    message: List operation {{path}} should support pageToken for pagination\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.name === 'pageToken')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\n  roblox-responses-have-error-schema:\n\
  \    description: Error responses should reference an error schema\n    message: Error response {{path}} should define a schema\n    severity: warn\n    given: \"$.paths[*][*].responses[4*].content[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  roblox-patch-uses-update-mask:\n    description: PATCH operations should support updateMask query parameter\n    message: PATCH operation {{path}} should support updateMask for partial updates\n    severity: info\n    given: \"$.paths[*].patch\"\n    then:\n      field: parameters\n      function: truthy\n\n  roblox-schema-has-description:\n    description: Schema components should have descriptions\n    message: Schema {{path}} is missing a description\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/roblox-engine-api/refs/heads/main/rules/roblox-open-cloud-rules.yml
tags:
- Gaming
- Game Development
- Metaverse
- Roblox
- Open Cloud
- Spectral
- Linting
- API Governance
---
