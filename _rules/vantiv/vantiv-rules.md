---
api_specs:
- filename: vantiv-cnp-openapi.yml
  format: yaml
  label: Vantiv CNP API
  slug: cnp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vantiv/refs/heads/main/openapi/vantiv-cnp-openapi.yml
- filename: vantiv-express-openapi.yml
  format: yaml
  label: Vantiv Express API
  slug: express-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vantiv/refs/heads/main/openapi/vantiv-express-openapi.yml
- filename: vantiv-chargeback-openapi.yml
  format: yaml
  label: Vantiv Chargeback API
  slug: chargeback-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vantiv/refs/heads/main/openapi/vantiv-chargeback-openapi.yml
categories:
- vantiv
description: Spectral linting rules defining API design standards and conventions for Vantiv.
layout: rules
name: Vantiv API Rules
provider_name: Vantiv
provider_slug: vantiv
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: vantiv-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: vantiv-operation-ids-present
  severity: error
- description: Transaction requests should include merchantId
  given: $.components.schemas[*].properties.merchantId
  name: vantiv-merchant-id-required
  severity: warn
- description: Transaction amounts are denominated in cents (integer)
  given: $.components.schemas[*].properties.amount
  name: vantiv-amount-in-cents
  severity: info
- description: Vantiv API uses application/xml content type
  given: $.paths[*][*].requestBody.content
  name: vantiv-xml-content-type
  severity: warn
- description: Operations should be tagged for grouping
  given: $.paths[*][*]
  name: vantiv-tags-defined
  severity: warn
- description: cnpTxnId fields should be int64 format
  given: $.components.schemas[*].properties.cnpTxnId
  name: vantiv-cnp-txn-id-int64
  severity: warn
- description: Vantiv uses HTTP Basic authentication
  given: $.components.securitySchemes.basicAuth
  name: vantiv-basic-auth-scheme
  severity: warn
rules_file: rules/vantiv-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vantiv/refs/heads/main/rules/vantiv-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 6
slug: vantiv-rules
source_filename: vantiv-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vantiv-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  vantiv-operation-ids-present:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  vantiv-merchant-id-required:\n    description: Transaction requests should include merchantId\n    severity: warn\n    given: \"$.components.schemas[*].properties.merchantId\"\n    then:\n      function: defined\n\n  vantiv-amount-in-cents:\n    description: Transaction amounts are denominated in cents (integer)\n    severity: info\n    given: \"$.components.schemas[*].properties.amount\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n\
  \          - integer\n\n  vantiv-xml-content-type:\n    description: Vantiv API uses application/xml content type\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"application/xml\"\n\n  vantiv-tags-defined:\n    description: Operations should be tagged for grouping\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  vantiv-cnp-txn-id-int64:\n    description: cnpTxnId fields should be int64 format\n    severity: warn\n    given: \"$.components.schemas[*].properties.cnpTxnId\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - int64\n\n  vantiv-basic-auth-scheme:\n    description: Vantiv uses HTTP Basic authentication\n    severity: warn\n    given: \"$.components.securitySchemes.basicAuth\"\n    then:\n      field: scheme\n      function: enumeration\n      functionOptions:\n\
  \        values:\n          - basic\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vantiv/refs/heads/main/rules/vantiv-rules.yml
tags:
- Payments
- Payment Processing
- eCommerce
- Finance
- FinTech
- Spectral
- Linting
- API Governance
---
