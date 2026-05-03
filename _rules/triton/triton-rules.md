---
api_specs:
- filename: rest_api.yaml
  format: yaml
  label: Triton HTTP/REST API
  slug: ''
  spec_type: OpenAPI
  url: https://github.com/triton-inference-server/server/blob/main/docs/protocol/rest_api.yaml
- filename: triton-metrics-openapi.yml
  format: yaml
  label: Triton Metrics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/triton/refs/heads/main/openapi/triton-metrics-openapi.yml
categories:
- triton
description: Spectral linting rules defining API design standards and conventions for Triton Inference Server.
layout: rules
name: Triton Inference Server API Rules
provider_name: Triton Inference Server
provider_slug: triton
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: triton-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: triton-require-tags
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: triton-require-description
  severity: warn
- description: All paths must begin with /v2 (KServe V2 protocol)
  given: $.paths[*]~
  name: triton-path-v2-prefix
  severity: error
- description: Path segments (excluding path parameters) should use snake_case or be known keywords
  given: $.paths[*]~
  name: triton-path-snake-case
  severity: info
- description: Error responses should define a schema
  given: $.paths[*][*].responses['400']
  name: triton-error-response-has-schema
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: triton-summary-title-case
  severity: warn
- description: Triton server endpoints are typically deployed without authentication (auth handled at network layer)
  given: $.paths[*][*].security
  name: triton-no-auth-required
  severity: info
rules_file: rules/triton-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/triton/refs/heads/main/rules/triton-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 5
slug: triton-rules
source_filename: triton-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Triton Inference Server API Convention Rules\n\n  triton-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase (e.g. modelInfer, repositoryIndex)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  triton-require-tags:\n    description: All operations must have at least one tag\n    message: Operations must be tagged (Health, Inference, Model Metadata, Model Repository, Statistics, etc.)\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  triton-require-description:\n    description: All operations must have a description\n    message: Operations must have a description\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  triton-path-v2-prefix:\n\
  \    description: All paths must begin with /v2 (KServe V2 protocol)\n    message: \"Path '{{value}}' must start with /v2\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2\"\n\n  triton-path-snake-case:\n    description: Path segments (excluding path parameters) should use snake_case or be known keywords\n    message: \"Path segments should use snake_case\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v2)(/[a-z0-9_{}]+)*$\"\n\n  triton-error-response-has-schema:\n    description: Error responses should define a schema\n    message: Error responses must define content schema\n    severity: warn\n    given: \"$.paths[*][*].responses['400']\"\n    then:\n      field: content\n      function: truthy\n\n  triton-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must\
  \ use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  triton-no-auth-required:\n    description: Triton server endpoints are typically deployed without authentication (auth handled at network layer)\n    message: Triton HTTP API has no authentication by default; document network-level security instead\n    severity: info\n    given: \"$.paths[*][*].security\"\n    then:\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/triton/refs/heads/main/rules/triton-rules.yml
tags:
- AI
- Deep Learning
- Inference
- Machine Learning
- Model Serving
- NVIDIA
- Open Source
- Spectral
- Linting
- API Governance
---
