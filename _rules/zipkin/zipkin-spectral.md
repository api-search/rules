---
api_specs:
- filename: zipkin-api-v2.yml
  format: yaml
  label: Zipkin API V2
  slug: zipkin-api-v2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zipkin/refs/heads/main/openapi/zipkin-api-v2.yml
categories:
- zipkin
description: Spectral linting rules defining API design standards and conventions for Zipkin.
layout: rules
name: Zipkin API Rules
provider_name: Zipkin
provider_slug: zipkin
rule_count: 6
rules:
- description: All operation summaries must start with "Zipkin"
  given: $.paths.*[get,post,put,delete,patch].summary
  name: zipkin-summary-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths.*[get,post,put,delete,patch]
  name: zipkin-operation-id
  severity: error
- description: Every operation must have at least one tag
  given: $.paths.*[get,post,put,delete,patch]
  name: zipkin-operation-tags
  severity: warn
- description: Every operation must have a description
  given: $.paths.*[get,post,put,delete,patch]
  name: zipkin-operation-description
  severity: warn
- description: traceId fields must use the hex pattern
  given: $.components.schemas.Span.properties.traceId.pattern
  name: zipkin-trace-id-pattern
  severity: warn
- description: Servers must be defined
  given: $.servers
  name: zipkin-server-url
  severity: error
rules_file: rules/zipkin-spectral.yaml
rules_url: https://raw.githubusercontent.com/api-evangelist/zipkin/refs/heads/main/rules/zipkin-spectral.yaml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 4
slug: zipkin-spectral
source_filename: zipkin-spectral.yaml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  zipkin-summary-prefix:\n    description: All operation summaries must start with \"Zipkin\"\n    message: \"Operation summary should start with 'Zipkin' provider prefix\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Zipkin \"\n  zipkin-operation-id:\n    description: Every operation must have an operationId\n    message: \"Operation must define an operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n  zipkin-operation-tags:\n    description: Every operation must have at least one tag\n    message: \"Operation must have a tag\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n  zipkin-operation-description:\n    description: Every operation must have a\
  \ description\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n  zipkin-trace-id-pattern:\n    description: traceId fields must use the hex pattern\n    severity: warn\n    given: \"$.components.schemas.Span.properties.traceId.pattern\"\n    then:\n      function: truthy\n  zipkin-server-url:\n    description: Servers must be defined\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zipkin/refs/heads/main/rules/zipkin-spectral.yaml
tags:
- Distributed Tracing
- Observability
- Open Source
- Microservices
- Spectral
- Linting
- API Governance
---
