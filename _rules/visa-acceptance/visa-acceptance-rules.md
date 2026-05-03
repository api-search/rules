---
api_specs:
- filename: visa-acceptance-payments-openapi.yml
  format: yaml
  label: Visa Acceptance Payments API
  slug: visa-acceptance-payments
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/visa-acceptance/refs/heads/main/openapi/visa-acceptance-payments-openapi.yml
- filename: visa-acceptance-payments-openapi.yml
  format: yaml
  label: Visa Acceptance Invoicing API
  slug: visa-acceptance-invoicing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/visa-acceptance/refs/heads/main/openapi/visa-acceptance-payments-openapi.yml
- filename: visa-acceptance-payments-openapi.yml
  format: yaml
  label: Visa Acceptance Pay by Link API
  slug: visa-acceptance-pay-by-link
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/visa-acceptance/refs/heads/main/openapi/visa-acceptance-payments-openapi.yml
categories:
- visa
description: Spectral linting rules defining API design standards and conventions for Visa Acceptance.
layout: rules
name: Visa Acceptance API Rules
provider_name: Visa Acceptance
provider_slug: visa-acceptance
rule_count: 8
rules:
- description: Operation IDs must use camelCase consistent with Visa Acceptance SDK conventions
  given: $.paths[*][*].operationId
  name: visa-acceptance-operation-id-case
  severity: warn
- description: All operations must have tags
  given: $.paths[*][*]
  name: visa-acceptance-tags-required
  severity: error
- description: Visa Acceptance represents monetary amounts as decimal strings to avoid floating-point precision issues
  given: $.components.schemas[*].properties.totalAmount
  name: visa-acceptance-amount-as-string
  severity: warn
- description: Payment-related follow-on operations should use paymentId path parameter
  given: $.paths['/pts/v2/payments/{paymentId}/captures','/pts/v2/payments/{paymentId}/refunds','/pts/v2/payments/{paymentId}/voids']
  name: visa-acceptance-payment-id-in-path
  severity: warn
- description: All server URLs must use HTTPS for payment security
  given: $.servers[*].url
  name: visa-acceptance-https-only
  severity: error
- description: All payment operations must require authentication
  given: $.paths[*][post,get,patch,delete]
  name: visa-acceptance-security-defined
  severity: error
- description: Payment endpoints should define error responses
  given: $.paths['/pts/v2/payments'][post]
  name: visa-acceptance-response-codes
  severity: warn
- description: Currency fields should use ISO 4217 format
  given: $.components.schemas[*].properties.currency
  name: visa-acceptance-currency-iso4217
  severity: info
rules_file: rules/visa-acceptance-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/visa-acceptance/refs/heads/main/rules/visa-acceptance-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: visa-acceptance-rules
source_filename: visa-acceptance-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  visa-acceptance-operation-id-case:\n    description: Operation IDs must use camelCase consistent with Visa Acceptance SDK conventions\n    message: \"Operation ID '{{value}}' should be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  visa-acceptance-tags-required:\n    description: All operations must have tags\n    message: \"Operation is missing tags\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  visa-acceptance-amount-as-string:\n    description: >-\n      Visa Acceptance represents monetary amounts as decimal strings to avoid\n      floating-point precision issues\n    message: \"Amount fields should be type string\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.totalAmount\"\n    then:\n      field: type\n      function: enumeration\n\
  \      functionOptions:\n        values:\n          - string\n\n  visa-acceptance-payment-id-in-path:\n    description: Payment-related follow-on operations should use paymentId path parameter\n    message: \"Follow-on operations should include paymentId in path\"\n    severity: warn\n    given: \"$.paths['/pts/v2/payments/{paymentId}/captures','/pts/v2/payments/{paymentId}/refunds','/pts/v2/payments/{paymentId}/voids']\"\n    then:\n      function: truthy\n\n  visa-acceptance-https-only:\n    description: All server URLs must use HTTPS for payment security\n    message: \"Server URL '{{value}}' must use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  visa-acceptance-security-defined:\n    description: All payment operations must require authentication\n    message: \"Operation must have security defined\"\n    severity: error\n    given: \"$.paths[*][post,get,patch,delete]\"\n\
  \    then:\n      field: security\n      function: truthy\n\n  visa-acceptance-response-codes:\n    description: Payment endpoints should define error responses\n    message: \"Payment operation should define 400 and 401 error responses\"\n    severity: warn\n    given: \"$.paths['/pts/v2/payments'][post]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['201', '400', '401']\n\n  visa-acceptance-currency-iso4217:\n    description: Currency fields should use ISO 4217 format\n    message: \"Currency field should be described as ISO 4217 3-letter code\"\n    severity: info\n    given: \"$.components.schemas[*].properties.currency\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/visa-acceptance/refs/heads/main/rules/visa-acceptance-rules.yml
tags:
- Payments
- E-Commerce
- Fintech
- Credit Cards
- Invoicing
- Payment Links
- Digital Wallets
- Spectral
- Linting
- API Governance
---
