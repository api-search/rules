---
api_specs:
- filename: tsys-payment-gateway-openapi.yml
  format: yaml
  label: TSYS Payment Gateway
  slug: tsys-payment-gateway
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/total-system-services/refs/heads/main/openapi/tsys-payment-gateway-openapi.yml
- filename: tsys-issuing-openapi.yml
  format: yaml
  label: TSYS Issuing Platform
  slug: tsys-issuing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/total-system-services/refs/heads/main/openapi/tsys-issuing-openapi.yml
categories:
- tsys
description: Spectral linting rules defining API design standards and conventions for Total System Services.
layout: rules
name: Total System Services API Rules
provider_name: Total System Services
provider_slug: total-system-services
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tsys-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tsys-operation-summary-title-case
  severity: warn
- description: API paths must use kebab-case
  given: $.paths[*]~
  name: tsys-paths-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: tsys-must-have-tags
  severity: error
- description: All operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tsys-must-have-200-or-201
  severity: error
- description: Payment endpoints must use security schemes
  given: $.paths[/transactions/authorize,/transactions/sale][post]
  name: tsys-payment-security
  severity: error
- description: Financial amount fields must use float format
  given: $.components.schemas[*].properties.amount
  name: tsys-financial-amount-format
  severity: warn
- description: Card number fields must be described as tokenized or masked
  given: $.components.schemas[*].properties.cardNumber
  name: tsys-pci-card-data
  severity: error
- description: List operations should support pagination
  given: $.paths[*][get][?(@.operationId =~ /^list/)]
  name: tsys-pagination-required
  severity: warn
- description: All operations must define error responses
  given: $.paths[*][post,put,delete].responses
  name: tsys-error-response-required
  severity: warn
rules_file: rules/tsys-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/total-system-services/refs/heads/main/rules/tsys-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: tsys-spectral-rules
source_filename: tsys-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  tsys-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tsys-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  tsys-paths-kebab-case:\n    description: API paths must use kebab-case\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-]+|/\\\\{[a-zA-Z0-9]+\\\\})*$\"\n\n  tsys-must-have-tags:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  tsys-must-have-200-or-201:\n\
  \    description: All operations must define a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  tsys-payment-security:\n    description: Payment endpoints must use security schemes\n    severity: error\n    given: \"$.paths[/transactions/authorize,/transactions/sale][post]\"\n    then:\n      field: security\n      function: truthy\n\n  tsys-financial-amount-format:\n    description: Financial amount fields must use float format\n    severity: warn\n    given: \"$.components.schemas[*].properties.amount\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            format:\n              enum: [\"float\", \"double\"]\n\n  tsys-pci-card-data:\n    description: Card number fields must be described as tokenized or masked\n\
  \    severity: error\n    given: \"$.components.schemas[*].properties.cardNumber\"\n    then:\n      field: description\n      function: truthy\n\n  tsys-pagination-required:\n    description: List operations should support pagination\n    severity: warn\n    given: \"$.paths[*][get][?(@.operationId =~ /^list/)]\"\n    then:\n      field: parameters\n      function: truthy\n\n  tsys-error-response-required:\n    description: All operations must define error responses\n    severity: warn\n    given: \"$.paths[*][post,put,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"404\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/total-system-services/refs/heads/main/rules/tsys-spectral-rules.yml
tags:
- Payments
- Payment Processing
- Card Issuing
- Merchant Services
- Fintech
- Financial Services
- Spectral
- Linting
- API Governance
---
