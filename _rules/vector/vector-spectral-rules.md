---
api_specs:
- filename: vector-observability-api-openapi.yml
  format: yaml
  label: Vector Observability API
  slug: vector-observability-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vector/refs/heads/main/openapi/vector-observability-api-openapi.yml
categories:
- health
- info
- 'no'
- openapi
- operation
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Vector.
layout: rules
name: Vector API Rules
provider_name: Vector
provider_slug: vector
rule_count: 16
rules:
- description: API title must be present.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Vector".
  given: $.info.title
  name: info-title-starts-with-vector
  severity: warn
- description: API description must be present.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x.
  given: $
  name: openapi-version-3x
  severity: error
- description: Servers array must be defined.
  given: $
  name: servers-required
  severity: error
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head]
  name: operation-operationId-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Vector".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-vector
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete,head]
  name: operation-description-required
  severity: warn
- description: Operations must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Schema definitions should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Observability API should expose a /health endpoint.
  given: $.paths
  name: health-endpoint-required
  severity: error
rules_file: rules/vector-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vector/refs/heads/main/rules/vector-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 7
slug: vector-spectral-rules
source_filename: vector-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-starts-with-vector:\n    description: API title should start with \"Vector\".\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Vector\"\n\n  info-description-required:\n    description: API description must be present.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3x:\n    description: Must use OpenAPI 3.x.\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n\
  \        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers array must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-description-required:\n    description: Each server should have a description.\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # OPERATIONS\n  operation-operationId-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-starts-with-vector:\n    description: Operation summaries should start with \"Vector\".\n\
  \    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Vector\"\n\n  operation-description-required:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head]\"\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least one 2xx response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  response-description-required:\n    description: All responses must have a description.\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n    \
  \  function: truthy\n\n  # SCHEMAS\n  schema-description-required:\n    description: Schema definitions should have descriptions.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  health-endpoint-required:\n    description: Observability API should expose a /health endpoint.\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: /health\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vector/refs/heads/main/rules/vector-spectral-rules.yml
tags:
- Data Pipeline
- Logs
- Metrics
- Observability
- Open Source
- Rust
- Traces
- Spectral
- Linting
- API Governance
---
