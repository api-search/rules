---
api_specs:
- filename: thanos-query-api.yml
  format: yaml
  label: Thanos Query API
  slug: thanos-query-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-query-api.yml
- filename: thanos-store-gateway-openapi.yml
  format: yaml
  label: Thanos Store Gateway API
  slug: thanos-store-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-store-gateway-openapi.yml
- filename: thanos-sidecar-openapi.yml
  format: yaml
  label: Thanos Sidecar API
  slug: thanos-sidecar-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-sidecar-openapi.yml
- filename: thanos-ruler-openapi.yml
  format: yaml
  label: Thanos Ruler API
  slug: thanos-ruler-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-ruler-openapi.yml
- filename: thanos-receive-openapi.yml
  format: yaml
  label: Thanos Receive API
  slug: thanos-receive-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-receive-openapi.yml
- filename: thanos-compact-openapi.yml
  format: yaml
  label: Thanos Compact API
  slug: thanos-compact-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/openapi/thanos-compact-openapi.yml
categories:
- thanos
description: Spectral linting rules defining API design standards and conventions for Thanos.
layout: rules
name: Thanos API Rules
provider_name: Thanos
provider_slug: thanos
rule_count: 8
rules:
- description: Prometheus-compatible API paths must start with /api/v1/
  given: $.paths[*]~
  name: thanos-prometheus-path-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete]
  name: thanos-operation-id-required
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: thanos-operation-id-camel-case
  severity: warn
- description: Successful responses should include content
  given: $.paths[*][get].responses.200
  name: thanos-200-has-content
  severity: warn
- description: Tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: thanos-tags-title-case
  severity: warn
- description: Summaries must use Title Case
  given: $.paths[*][*].summary
  name: thanos-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,delete]
  name: thanos-operation-description
  severity: warn
- description: GET operations should not have a request body (use POST variants for long queries)
  given: $.paths[*].get
  name: thanos-get-no-body
  severity: warn
rules_file: rules/thanos-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/rules/thanos-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 7
slug: thanos-rules
source_filename: thanos-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Thanos: Prometheus-compatible paths must use /api/v1/ prefix\n  thanos-prometheus-path-prefix:\n    description: Prometheus-compatible API paths must start with /api/v1/\n    message: Prometheus-compatible path \"{{value}}\" must start with /api/v1/ or /-/\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/api/v1/|/-/|/metrics)\"\n\n  # Thanos: Operations must have operationIds\n  thanos-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Thanos: operationIds must be camelCase\n  thanos-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: OperationId \"{{value}}\" should use camelCase\n    severity: warn\n    given:\
  \ \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Thanos: Successful responses must include content\n  thanos-200-has-content:\n    description: Successful responses should include content\n    message: Response 200 should include content definition\n    severity: warn\n    given: \"$.paths[*][get].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  # Thanos: Tags must use Title Case\n  thanos-tags-title-case:\n    description: Tags must use Title Case\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # Thanos: Summaries must be Title Case\n  thanos-summary-title-case:\n    description: Summaries must use Title Case\n    message: Summary \"{{value}}\" should use Title Case\n    severity: warn\n\
  \    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Thanos: All operations must have descriptions\n  thanos-operation-description:\n    description: All operations must have a description\n    message: Operation is missing a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Thanos: GET operations must not have a request body\n  thanos-get-no-body:\n    description: GET operations should not have a request body (use POST variants for long queries)\n    message: GET operation should not include requestBody\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thanos/refs/heads/main/rules/thanos-rules.yml
tags:
- Metrics
- Monitoring
- Observability
- Prometheus
- Time Series Database
- Spectral
- Linting
- API Governance
---
