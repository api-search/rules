---
api_specs:
- filename: trabex-trade-compliance-openapi.yml
  format: yaml
  label: Trabex Trade Compliance API
  slug: trade-compliance
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trabex/refs/heads/main/openapi/trabex-trade-compliance-openapi.yml
categories:
- trabex
description: Spectral linting rules defining API design standards and conventions for Trabex.
layout: rules
name: Trabex API Rules
provider_name: Trabex
provider_slug: trabex
rule_count: 11
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: trabex-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: trabex-operation-ids-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][*]
  name: trabex-operation-description-required
  severity: warn
- description: API key authentication must use X-API-Key header.
  given: $.components.securitySchemes.apiKeyAuth
  name: trabex-api-key-in-header
  severity: warn
- description: All operations must be tagged for categorization.
  given: $.paths[*][*]
  name: trabex-tags-required
  severity: warn
- description: All API paths must be versioned with /v1/ prefix.
  given: $.paths[*]~
  name: trabex-versioned-paths
  severity: error
- description: Paths with shipmentId must define it as a path parameter.
  given: $.paths[*][*].parameters[?(@.name=='shipmentId')]
  name: trabex-shipment-id-path-param
  severity: error
- description: All operations must define a 200 or 201 success response.
  given: $.paths[*][*].responses
  name: trabex-response-2xx-defined
  severity: error
- description: All operations should define a 401 unauthorized response.
  given: $.paths[*][*].responses
  name: trabex-response-401-defined
  severity: warn
- description: POST and PUT operations must define a requestBody.
  given: $.paths[*][post,put]
  name: trabex-post-request-body
  severity: error
- description: Screening responses must include riskLevel field.
  given: $.components.schemas.ScreeningResponse.properties
  name: trabex-screening-response-risk-level
  severity: warn
rules_file: rules/trabex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trabex/refs/heads/main/rules/trabex-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 6
slug: trabex-rules
source_filename: trabex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trabex-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  trabex-operation-ids-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: defined\n\n  trabex-operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: defined\n\n  trabex-api-key-in-header:\n    description: API key authentication must use X-API-Key header.\n    severity: warn\n    given: \"$.components.securitySchemes.apiKeyAuth\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n \
  \         type: object\n          properties:\n            in:\n              const: header\n            name:\n              const: X-API-Key\n\n  trabex-tags-required:\n    description: All operations must be tagged for categorization.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  trabex-versioned-paths:\n    description: All API paths must be versioned with /v1/ prefix.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  trabex-shipment-id-path-param:\n    description: Paths with shipmentId must define it as a path parameter.\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name=='shipmentId')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            in:\n              const: path\n            required:\n              const: true\n\n \
  \ trabex-response-2xx-defined:\n    description: All operations must define a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  trabex-response-401-defined:\n    description: All operations should define a 401 unauthorized response.\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  trabex-post-request-body:\n    description: POST and PUT operations must define a requestBody.\n    severity: error\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: defined\n\n  trabex-screening-response-risk-level:\n    description: Screening responses must include riskLevel field.\n    severity: warn\n    given: \"$.components.schemas.ScreeningResponse.properties\"\
  \n    then:\n      field: riskLevel\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trabex/refs/heads/main/rules/trabex-rules.yml
tags:
- Compliance
- Export Control
- Logistics
- Restricted Party Screening
- Shipment Management
- Trade Compliance
- Spectral
- Linting
- API Governance
---
