---
api_specs:
- filename: scansource-product-openapi.yml
  format: yaml
  label: ScanSource Product API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scansource/refs/heads/main/openapi/scansource-product-openapi.yml
- filename: scansource-sales-order-openapi.yml
  format: yaml
  label: ScanSource Sales Order API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scansource/refs/heads/main/openapi/scansource-sales-order-openapi.yml
- filename: scansource-invoice-openapi.yml
  format: yaml
  label: ScanSource Invoice API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scansource/refs/heads/main/openapi/scansource-invoice-openapi.yml
categories:
- scansource
description: Spectral linting rules defining API design standards and conventions for ScanSource.
layout: rules
name: ScanSource API Rules
provider_name: ScanSource
provider_slug: scansource
rule_count: 10
rules:
- description: Customer number must be provided for all customer-scoped operations
  given: $.paths[*][get,post,delete]
  name: scansource-customer-number-required
  severity: error
- description: All ScanSource API operations must require the subscription key
  given: $.paths[*][get,post,put,patch,delete]
  name: scansource-api-key-security
  severity: error
- description: List operations should support pagination via page and pageSize parameters
  given: $.paths[*list*,*summary*][get]
  name: scansource-pagination-parameters
  severity: warn
- description: Batch requests must not exceed 40 items
  given: $.paths['/product/availability','product/pricing'].post.requestBody.content.application/json.schema.properties.items
  name: scansource-batch-size-limit
  severity: warn
- description: Customer-scoped paths should include customerNumber as a path parameter
  given: $.paths[*/{customerNumber}*]
  name: scansource-customer-number-path
  severity: warn
- description: List responses should include totalCount for pagination support
  given: $.components.schemas[*Response]
  name: scansource-response-envelope
  severity: warn
- description: Date filter parameters must use ISO 8601 date format
  given: $.paths[*][get].parameters[?(@.name == 'fromDate' || @.name == 'toDate')]
  name: scansource-date-filter-format
  severity: error
- description: All operations must have operationId in camelCase
  given: $.paths[*][get,post,put,patch,delete]
  name: scansource-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: scansource-tags-required
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: scansource-summaries-title-case
  severity: warn
rules_file: rules/scansource-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scansource/refs/heads/main/rules/scansource-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: scansource-rules
source_filename: scansource-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  scansource-customer-number-required:\n    description: Customer number must be provided for all customer-scoped operations\n    message: \"Operations that return customer-specific data must include customerNumber as a required parameter\"\n    severity: error\n    given: \"$.paths[*][get,post,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  scansource-api-key-security:\n    description: All ScanSource API operations must require the subscription key\n    message: \"Operations must use ApiKeyAuth (Ocp-Apim-Subscription-Key) security\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  scansource-pagination-parameters:\n    description: List operations should support pagination via page and pageSize parameters\n    message: \"List and summary endpoints should include page and pageSize query parameters\"\n    severity:\
  \ warn\n    given: \"$.paths[*list*,*summary*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  scansource-batch-size-limit:\n    description: Batch requests must not exceed 40 items\n    message: \"Availability and pricing batch requests should document a maximum of 40 items per request\"\n    severity: warn\n    given: \"$.paths['/product/availability','product/pricing'].post.requestBody.content.application/json.schema.properties.items\"\n    then:\n      field: maxItems\n      function: truthy\n\n  scansource-customer-number-path:\n    description: Customer-scoped paths should include customerNumber as a path parameter\n    message: \"Customer-scoped resource paths should have customerNumber in the path\"\n    severity: warn\n    given: \"$.paths[*/{customerNumber}*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  scansource-response-envelope:\n    description: List\
  \ responses should include totalCount for pagination support\n    message: \"Collection responses should include totalCount, page, and pageSize fields\"\n    severity: warn\n    given: \"$.components.schemas[*Response]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  scansource-date-filter-format:\n    description: Date filter parameters must use ISO 8601 date format\n    message: \"Date parameters should use format: date (ISO 8601)\"\n    severity: error\n    given: \"$.paths[*][get].parameters[?(@.name == 'fromDate' || @.name == 'toDate')]\"\n    then:\n      field: schema.format\n      function: pattern\n      functionOptions:\n        match: \"^date$\"\n\n  scansource-operation-ids:\n    description: All operations must have operationId in camelCase\n    message: \"OperationId must be defined and use camelCase\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n\
  \      function: truthy\n\n  scansource-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operations must include tags for categorization\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  scansource-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Operation summary should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scansource/refs/heads/main/rules/scansource-rules.yml
tags:
- ScanSource
- Distribution
- Barcode
- Point Of Sale
- AIDC
- Inventory
- Order Management
- E-Commerce
- Spectral
- Linting
- API Governance
---
