---
api_specs:
- filename: tempo-openapi.yml
  format: yaml
  label: Tempo HTTP API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tempo/refs/heads/main/openapi/tempo-openapi.yml
categories:
- tempo
description: Spectral linting rules defining API design standards and conventions for Tempo.
layout: rules
name: Tempo API Rules
provider_name: Tempo
provider_slug: tempo
rule_count: 9
rules:
- description: Tempo HTTP API is an internal service API without authentication by design
  given: $.paths[*][get,post,put,delete].security
  name: tempo-no-auth-required
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: tempo-operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: tempo-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tempo-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: tempo-operation-tags-required
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: tempo-operation-description-required
  severity: warn
- description: traceID path parameters should enforce hex format
  given: $.paths[*].parameters[?(@.name=='traceID')].schema
  name: tempo-traceid-pattern
  severity: warn
- description: API spec must define server URLs
  given: $
  name: tempo-server-urls-required
  severity: error
- description: Successful responses should include a schema
  given: $.paths[*][get].responses.200.content.application/json
  name: tempo-success-response-schema
  severity: warn
rules_file: rules/tempo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tempo/refs/heads/main/rules/tempo-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: tempo-rules
source_filename: tempo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Tempo API has no auth - all operations should be public (internal service)\n  tempo-no-auth-required:\n    description: Tempo HTTP API is an internal service API without authentication by design\n    message: \"Tempo API operations should not require authentication — it is an internal service\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete].security\"\n    then:\n      function: falsy\n\n  # Enforce operation IDs\n  tempo-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Enforce camelCase operation IDs\n  tempo-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Enforce Title Case summaries\n  tempo-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Enforce tags\n  tempo-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Enforce descriptions\n  tempo-operation-description-required:\n    description: All operations must have a description\n    message: \"Operation is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  # TraceID path parameters should have hex pattern validation\n  tempo-traceid-pattern:\n    description: traceID path parameters should enforce hex format\n    message: \"traceID parameter should have hex format pattern\"\n    severity: warn\n    given: \"$.paths[*].parameters[?(@.name=='traceID')].schema\"\n    then:\n      field: pattern\n      function: truthy\n\n  # Server URLs required\n  tempo-server-urls-required:\n    description: API spec must define server URLs\n    message: \"API spec is missing server definitions\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  # 200 responses must have schemas\n  tempo-success-response-schema:\n    description: Successful responses should include a schema\n    message: \"200 response is missing a schema\"\n    severity: warn\n    given: \"$.paths[*][get].responses.200.content.application/json\"\n    then:\n      field: schema\n\
  \      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tempo/refs/heads/main/rules/tempo-rules.yml
tags:
- Distributed Tracing
- Observability
- OpenTelemetry
- Grafana
- Monitoring
- Spectral
- Linting
- API Governance
---
