---
api_specs:
- filename: zenml-openapi.yml
  format: yaml
  label: ZenML OSS REST API
  slug: zenml-oss-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zenml/refs/heads/main/openapi/zenml-openapi.yml
categories:
- zenml
description: Spectral linting rules defining API design standards and conventions for ZenML.
layout: rules
name: ZenML API Rules
provider_name: ZenML
provider_slug: zenml
rule_count: 6
rules:
- description: Operation IDs MUST be camelCase
  given: $.paths[*][*].operationId
  name: zenml-operation-id-camelcase
  severity: error
- description: Operation summaries MUST be in Title Case.
  given: $.paths[*][*].summary
  name: zenml-summary-title-case
  severity: warn
- description: Every operation MUST have at least one tag.
  given: $.paths[*][*]
  name: zenml-tag-required
  severity: error
- description: Operations MUST require bearer authentication unless explicitly public.
  given: $
  name: zenml-bearer-auth-required
  severity: warn
- description: List operations should expose page and size query parameters.
  given: $.paths[*].get.parameters
  name: zenml-pagination-params
  severity: info
- description: Resource path identifiers MUST be UUIDs.
  given: $.paths[?(@property.match(/\{[a-z_]+_id\}/))]
  name: zenml-uuid-path-ids
  severity: warn
rules_file: rules/zenml-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/zenml/refs/heads/main/rules/zenml-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 3
slug: zenml-rules
source_filename: zenml-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  zenml-operation-id-camelcase:\n    description: Operation IDs MUST be camelCase\n    given: $.paths[*][*].operationId\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n  zenml-summary-title-case:\n    description: Operation summaries MUST be in Title Case.\n    given: $.paths[*][*].summary\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*( [A-Z][A-Za-z0-9]*)*$\"\n  zenml-tag-required:\n    description: Every operation MUST have at least one tag.\n    given: $.paths[*][*]\n    severity: error\n    then:\n      field: tags\n      function: truthy\n  zenml-bearer-auth-required:\n    description: Operations MUST require bearer authentication unless explicitly public.\n    given: $\n    severity: warn\n    then:\n      field: components.securitySchemes.bearerAuth\n      function: truthy\n  zenml-pagination-params:\n\
  \    description: List operations should expose page and size query parameters.\n    given: $.paths[*].get.parameters\n    severity: info\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n  zenml-uuid-path-ids:\n    description: Resource path identifiers MUST be UUIDs.\n    given: $.paths[?(@property.match(/\\{[a-z_]+_id\\}/))]\n    severity: warn\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zenml/refs/heads/main/rules/zenml-rules.yml
tags:
- AI
- Machine Learning
- MLOps
- LLMOps
- Pipelines
- Open Source
- Python
- Spectral
- Linting
- API Governance
---
