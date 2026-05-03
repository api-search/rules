---
api_specs:
- filename: signoz-openapi.yml
  format: yaml
  label: SigNoz
  slug: signoz
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/signoz/refs/heads/main/openapi/signoz-openapi.yml
categories:
- signoz
description: Spectral linting rules defining API design standards and conventions for SigNoz.
layout: rules
name: SigNoz API Rules
provider_name: SigNoz
provider_slug: signoz
rule_count: 8
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: signoz-operation-summary-title-case
  severity: warn
- description: OperationIds must use kebab-case naming.
  given: $.paths[*][*].operationId
  name: signoz-operation-id-kebab-case
  severity: warn
- description: API key authentication must use SigNoz-Api-Key header.
  given: $.components.securitySchemes[?(@.type=='apiKey')].name
  name: signoz-api-key-header
  severity: warn
- description: All paths must begin with /api/v prefix.
  given: $.paths[*]~
  name: signoz-paths-use-api-prefix
  severity: warn
- description: All responses should return application/json content type.
  given: $.paths[*][*].responses[*].content
  name: signoz-response-json
  severity: info
- description: Operations should reference tags defined at the top level.
  given: $.paths[*][*].tags[*]
  name: signoz-tags-defined
  severity: warn
- description: Error responses (4xx/5xx) should have a consistent schema.
  given: $.paths[*][*].responses[?(@property >= '400')].content['application/json'].schema
  name: signoz-error-response-schema
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][*].parameters[?(@.in=='query' || @.in=='path')]
  name: signoz-parameters-described
  severity: info
rules_file: rules/signoz-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/signoz/refs/heads/main/rules/signoz-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 2
  warn: 6
slug: signoz-rules
source_filename: signoz-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  signoz-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  signoz-operation-id-kebab-case:\n    description: OperationIds must use kebab-case naming.\n    message: \"OperationId '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9]*(-[a-z0-9]+)*$\"\n\n  signoz-api-key-header:\n    description: API key authentication must use SigNoz-Api-Key header.\n    message: \"API key authentication should use SigNoz-Api-Key header name.\"\n    severity: warn\n    given: \"$.components.securitySchemes[?(@.type=='apiKey')].name\"\n    then:\n\
  \      function: enumeration\n      functionOptions:\n        values:\n          - SigNoz-Api-Key\n\n  signoz-paths-use-api-prefix:\n    description: All paths must begin with /api/v prefix.\n    message: \"Path '{{property}}' must start with /api/v.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+\"\n\n  signoz-response-json:\n    description: All responses should return application/json content type.\n    message: \"Response should include application/json content type.\"\n    severity: info\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"application/json\"\n\n  signoz-tags-defined:\n    description: Operations should reference tags defined at the top level.\n    message: \"Operation tags should match top-level tag definitions.\"\n    severity: warn\n  \
  \  given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: truthy\n\n  signoz-error-response-schema:\n    description: Error responses (4xx/5xx) should have a consistent schema.\n    message: \"Error response should have a defined schema.\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '400')].content['application/json'].schema\"\n    then:\n      function: truthy\n\n  signoz-parameters-described:\n    description: All parameters must have a description.\n    message: \"Parameter '{{property}}' is missing a description.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in=='query' || @.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/signoz/refs/heads/main/rules/signoz-rules.yml
tags:
- APM
- Alerting
- Cloud Monitoring
- Dashboards
- Distributed Tracing
- Infrastructure Monitoring
- Logs
- Metrics
- Observability
- OpenTelemetry
- Open Source
- Spectral
- Linting
- API Governance
---
