---
api_specs:
- filename: valueray-symbol-data-openapi.yml
  format: yaml
  label: ValueRay Symbol Data API
  slug: symbol-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/valueray/refs/heads/main/openapi/valueray-symbol-data-openapi.yml
categories:
- valueray
description: Spectral linting rules defining API design standards and conventions for ValueRay.
layout: rules
name: ValueRay API Rules
provider_name: ValueRay
provider_slug: valueray
rule_count: 8
rules:
- description: Info object MUST include a contact pointing at ValueRay.
  given: $.info
  name: valueray-info-contact
  severity: error
- description: Servers MUST point at the canonical ValueRay API v1 base URL.
  given: $.servers[*]
  name: valueray-server-base-url
  severity: error
- description: Operation summaries MUST be Title Case.
  given: $.paths.*.*.summary
  name: valueray-operation-summary-title-case
  severity: warn
- description: Operation IDs MUST be camelCase.
  given: $.paths.*.*.operationId
  name: valueray-operation-id-camelcase
  severity: error
- description: Symbol-scoped operations MUST require a symbol query parameter.
  given: $.paths['/symbolData'].get.parameters[?(@.name=='symbol')]
  name: valueray-symbol-parameter-required
  severity: error
- description: Operation tags MUST come from the published tag set.
  given: $.paths.*.*.tags[*]
  name: valueray-tag-allowlist
  severity: warn
- description: SymbolDataResponse MUST include a disclaimer field.
  given: $.components.schemas.SymbolDataResponse
  name: valueray-disclaimer-property
  severity: error
- description: SymbolDataResponse MUST include a field_explanations URI.
  given: $.components.schemas.SymbolDataResponse
  name: valueray-field-explanations-property
  severity: error
rules_file: rules/valueray-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/valueray/refs/heads/main/rules/valueray-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 2
slug: valueray-rules
source_filename: valueray-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [\"spectral:oas\"]\ndocumentationUrl: https://www.valueray.com/api\nrules:\n  valueray-info-contact:\n    description: Info object MUST include a contact pointing at ValueRay.\n    severity: error\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  valueray-server-base-url:\n    description: Servers MUST point at the canonical ValueRay API v1 base URL.\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://www\\\\.valueray\\\\.com/api/v1$\"\n\n  valueray-operation-summary-title-case:\n    description: Operation summaries MUST be Title Case.\n    severity: warn\n    given: $.paths.*.*.summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-zA-Z0-9]*)( [A-Z][a-zA-Z0-9]*)*$\"\n\n  valueray-operation-id-camelcase:\n    description: Operation IDs MUST be camelCase.\n    severity: error\n    given: $.paths.*.*.operationId\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  valueray-symbol-parameter-required:\n    description: Symbol-scoped operations MUST require a symbol query parameter.\n    severity: error\n    given: $.paths['/symbolData'].get.parameters[?(@.name=='symbol')]\n    then:\n      field: required\n      function: truthy\n\n  valueray-tag-allowlist:\n    description: Operation tags MUST come from the published tag set.\n    severity: warn\n    given: $.paths.*.*.tags[*]\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Symbol Data\n\n  valueray-disclaimer-property:\n    description: SymbolDataResponse MUST include a disclaimer field.\n    severity: error\n    given: $.components.schemas.SymbolDataResponse\n    then:\n      field: required\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: disclaimer\n\n  valueray-field-explanations-property:\n\
  \    description: SymbolDataResponse MUST include a field_explanations URI.\n    severity: error\n    given: $.components.schemas.SymbolDataResponse\n    then:\n      field: required\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: field_explanations\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/valueray/refs/heads/main/rules/valueray-rules.yml
tags:
- AI/LLM
- ETF
- Financial Data
- Quantitative
- Stocks
- Technical Analysis
- Spectral
- Linting
- API Governance
---
