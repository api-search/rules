---
api_specs:
- filename: teller-openapi.yml
  format: yaml
  label: Teller API
  slug: teller-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/teller/refs/heads/main/openapi/teller-openapi.yml
categories:
- teller
description: Spectral linting rules defining API design standards and conventions for Teller.
layout: rules
name: Teller API Rules
provider_name: Teller
provider_slug: teller
rule_count: 12
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: teller-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: teller-operation-must-have-operationid
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: teller-operationid-camelcase
  severity: warn
- description: Server URL must use api.teller.io
  given: $.servers[*].url
  name: teller-server-must-be-api-teller
  severity: error
- description: Account ID path parameters should be named account_id
  given: $.paths['/accounts/{account_id}'][*].parameters[?(@.in == 'path')]
  name: teller-account-id-path-parameter
  severity: warn
- description: All authenticated operations must handle 401 Unauthorized
  given: $.paths['/accounts'][get].responses
  name: teller-response-must-have-401
  severity: error
- description: GET operations should handle 429 rate limiting
  given: $.paths[*].get.responses
  name: teller-response-must-have-429
  severity: warn
- description: DELETE operations must return 204 No Content
  given: $.paths[*].delete.responses
  name: teller-delete-returns-204
  severity: error
- description: Financial amounts should be represented as string type to preserve precision
  given: $.components.schemas[*].properties.amount
  name: teller-amount-as-string
  severity: warn
- description: Transaction status must use approved enum values
  given: $.components.schemas.Transaction.properties.status
  name: teller-transaction-status-enum
  severity: error
- description: Account type must use approved enum values
  given: $.components.schemas.Account.properties.type
  name: teller-account-type-enum
  severity: error
- description: Security scheme must use bearer type for mTLS access tokens
  given: $.components.securitySchemes.BearerMtls
  name: teller-bearer-mtls-security-scheme
  severity: error
rules_file: rules/teller-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/teller/refs/heads/main/rules/teller-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 5
slug: teller-rules
source_filename: teller-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  teller-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  teller-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  teller-operationid-camelcase:\n    description: Operation IDs should use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  teller-server-must-be-api-teller:\n    description: Server URL must use api.teller.io\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.teller\\\\.io\"\
  \n\n  teller-account-id-path-parameter:\n    description: Account ID path parameters should be named account_id\n    severity: warn\n    given: \"$.paths['/accounts/{account_id}'][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - account_id\n\n  teller-response-must-have-401:\n    description: All authenticated operations must handle 401 Unauthorized\n    severity: error\n    given: \"$.paths['/accounts'][get].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  teller-response-must-have-429:\n    description: GET operations should handle 429 rate limiting\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: '429'\n      function: truthy\n\n  teller-delete-returns-204:\n    description: DELETE operations must return 204 No Content\n    severity: error\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: '204'\n      function:\
  \ truthy\n\n  teller-amount-as-string:\n    description: >-\n      Financial amounts should be represented as string type to preserve precision\n    severity: warn\n    given: \"$.components.schemas[*].properties.amount\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  teller-transaction-status-enum:\n    description: Transaction status must use approved enum values\n    severity: error\n    given: \"$.components.schemas.Transaction.properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  teller-account-type-enum:\n    description: Account type must use approved enum values\n    severity: error\n    given: \"$.components.schemas.Account.properties.type\"\n    then:\n      field: enum\n      function: truthy\n\n  teller-bearer-mtls-security-scheme:\n    description: Security scheme must use bearer type for mTLS access tokens\n    severity: error\n    given: \"$.components.securitySchemes.BearerMtls\"\
  \n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/teller/refs/heads/main/rules/teller-rules.yml
tags:
- Banking
- Financial Data
- FinTech
- Open Banking
- Transactions
- Unified API
- Spectral
- Linting
- API Governance
---
