---
api_specs:
- filename: truelayer-payments-openapi.yml
  format: yaml
  label: TrueLayer Payments API
  slug: payments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truelayer/refs/heads/main/openapi/truelayer-payments-openapi.yml
categories:
- truelayer
description: Spectral linting rules defining API design standards and conventions for TrueLayer.
layout: rules
name: TrueLayer API Rules
provider_name: TrueLayer
provider_slug: truelayer
rule_count: 11
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: truelayer-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: truelayer-operation-tags-required
  severity: error
- description: All paths must use the /v3/ prefix
  given: $.paths[*]~
  name: truelayer-v3-path-prefix
  severity: error
- description: POST operations must require an Idempotency-Key header
  given: $.paths[*][post].parameters[*]
  name: truelayer-idempotency-key-required
  severity: error
- description: POST payment operations require Tl-Signature header
  given: $.paths[/v3/payments,/v3/mandates,/v3/payouts][post].parameters
  name: truelayer-signature-header-post
  severity: error
- description: Payment amounts must be in minor units (integer), not decimal
  given: $.components.schemas.*.properties.amount_in_minor
  name: truelayer-amount-minor-units
  severity: error
- description: Currency fields must be restricted to supported values (GBP, EUR)
  given: $.components.schemas.*.properties.currency
  name: truelayer-currency-enum
  severity: warn
- description: ID fields should use UUID format
  given: $.components.schemas.*.properties.id
  name: truelayer-uuid-format
  severity: hint
- description: Webhook types should be documented as enum values
  given: $.components.schemas.*.properties.type
  name: truelayer-webhook-type-documented
  severity: hint
- description: Error responses should include a trace_id for debugging
  given: $.paths[*][*].responses[4*,5*].content.application/json.schema.properties
  name: truelayer-error-trace-id
  severity: hint
- description: All operations must define a 200 success response
  given: $.paths[*][get,post,delete]
  name: truelayer-success-2xx-defined
  severity: error
rules_file: rules/truelayer-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/truelayer/refs/heads/main/rules/truelayer-rules.yml
severity_counts:
  error: 6
  hint: 3
  info: 0
  warn: 2
slug: truelayer-rules
source_filename: truelayer-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  truelayer-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]* ?)+$\"\n\n  truelayer-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  truelayer-v3-path-prefix:\n    description: All paths must use the /v3/ prefix\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v3/\"\n\n  truelayer-idempotency-key-required:\n    description: POST operations must require an Idempotency-Key header\n    severity: error\n    given: \"$.paths[*][post].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \          properties:\n            name:\n              type: string\n\n  truelayer-signature-header-post:\n    description: POST payment operations require Tl-Signature header\n    severity: error\n    given: \"$.paths[/v3/payments,/v3/mandates,/v3/payouts][post].parameters\"\n    then:\n      function: truthy\n\n  truelayer-amount-minor-units:\n    description: >-\n      Payment amounts must be in minor units (integer), not decimal\n    severity: error\n    given: \"$.components.schemas.*.properties.amount_in_minor\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  truelayer-currency-enum:\n    description: Currency fields must be restricted to supported values (GBP, EUR)\n    severity: warn\n    given: \"$.components.schemas.*.properties.currency\"\n    then:\n      field: enum\n      function: truthy\n\n  truelayer-uuid-format:\n    description: ID fields should use UUID format\n    severity: hint\n    given:\
  \ \"$.components.schemas.*.properties.id\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - uuid\n\n  truelayer-webhook-type-documented:\n    description: Webhook types should be documented as enum values\n    severity: hint\n    given: \"$.components.schemas.*.properties.type\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  truelayer-error-trace-id:\n    description: Error responses should include a trace_id for debugging\n    severity: hint\n    given: \"$.paths[*][*].responses[4*,5*].content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  truelayer-success-2xx-defined:\n    description: All operations must define a 200 success response\n    severity: error\n    given: \"$.paths[*][get,post,delete]\"\n    then:\n \
  \     field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/truelayer/refs/heads/main/rules/truelayer-rules.yml
tags:
- Data API
- Financial Services
- Open Banking
- Payments
- PSD2
- UK Banking
- VRP
- Spectral
- Linting
- API Governance
---
