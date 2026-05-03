---
api_specs:
- filename: sap-concur-expense-report-openapi.yml
  format: yaml
  label: Expense Report v3 API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/openapi/sap-concur-expense-report-openapi.yml
- filename: sap-concur-expense-report-openapi.yml
  format: yaml
  label: Expense Entry v3 API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/openapi/sap-concur-expense-report-openapi.yml
- filename: sap-concur-expense-report-openapi.yml
  format: yaml
  label: Quick Expense v3 API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/openapi/sap-concur-expense-report-openapi.yml
- filename: sap-concur-expense-report-openapi.yml
  format: yaml
  label: Receipt Image v3 API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/openapi/sap-concur-expense-report-openapi.yml
categories:
- concur
description: Spectral linting rules defining API design standards and conventions for SAP Concur Expense.
layout: rules
name: SAP Concur Expense API Rules
provider_name: SAP Concur Expense
provider_slug: sap-concur-expense
rule_count: 16
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: concur-operation-id-required
  severity: error
- description: SAP Concur operation IDs use camelCase (e.g., listExpenseReports, createExpenseEntry, getPaymentBatch)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: concur-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case (e.g., Expense Reports, Quick Expenses)
  given: $.tags[*].name
  name: concur-tags-title-case
  severity: warn
- description: SAP Concur API paths use lowercase kebab-case for multi-word resource names (e.g., /expense/quickexpenses, /expense/receiptimages)
  given: $.paths[*]~
  name: concur-path-kebab-case
  severity: warn
- description: All 200 responses must have a response schema defined
  given: $.paths[*][get,post].responses['200']
  name: concur-response-200-has-schema
  severity: warn
- description: Collection endpoints (GET returning arrays) should support limit parameter for pagination (max 100 per SAP Concur convention)
  given: $.paths[*].get.parameters[?(@.name=='limit')]
  name: concur-pagination-limit-param
  severity: hint
- description: Collection endpoints should support offset parameter for cursor-based pagination using the NextPage URL pattern
  given: $.paths[*].get
  name: concur-pagination-offset-param
  severity: hint
- description: Currency code fields must be ISO 4217 three-letter uppercase codes. SAP Concur uses CurrencyCode and TransactionCurrencyCode naming.
  given: $.components.schemas[*].properties[?(@property.match(/CurrencyCode$/))]
  name: concur-currency-code-format
  severity: hint
- description: SAP Concur uses string identifiers (hex GUIDs) for all resource IDs. ID fields must be typed as string, not integer.
  given: $.components.schemas[*].properties.ID
  name: concur-id-field-type-string
  severity: error
- description: Expense entry endpoints require reportID as a query parameter when listing entries. The ReportID parameter enables server-side filtering.
  given: $.paths['/expense/entries'].get.parameters[?(@.name=='reportID')]
  name: concur-report-id-references
  severity: hint
- description: DELETE operations in SAP Concur APIs return 204 No Content on success (not 200). Ensure DELETE responses use 204.
  given: $.paths[*].delete.responses
  name: concur-delete-returns-204
  severity: warn
- description: PUT update operations in SAP Concur APIs return 204 No Content on success. The full updated resource is retrieved via a subsequent GET.
  given: $.paths[*].put.responses
  name: concur-put-returns-204
  severity: warn
- description: POST create operations return 200 with an ID response body rather than 201. This follows SAP Concur v3 API conventions.
  given: $.paths[*].post.responses
  name: concur-post-create-returns-200
  severity: info
- description: SAP Concur APIs require OAuth 2.0 authentication. All operations should reference the OAuth2 security scheme.
  given: $.components.securitySchemes
  name: concur-oauth2-security-defined
  severity: warn
- description: Path parameters for resource IDs should be named 'id' (lowercase) following SAP Concur conventions.
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: concur-entry-id-path-param
  severity: hint
- description: Date fields should use ISO 8601 format. Transaction dates use date format, datetime fields use date-time format.
  given: $.components.schemas[*].properties[?(@property.match(/Date$/))]
  name: concur-date-fields-iso8601
  severity: warn
rules_file: rules/sap-concur-expense-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/rules/sap-concur-expense-rules.yml
severity_counts:
  error: 2
  hint: 5
  info: 1
  warn: 8
slug: sap-concur-expense-rules
source_filename: sap-concur-expense-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SAP Concur Expense API Naming Conventions\n  concur-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  concur-operation-id-camel-case:\n    description: >-\n      SAP Concur operation IDs use camelCase (e.g., listExpenseReports,\n      createExpenseEntry, getPaymentBatch)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  concur-tags-title-case:\n    description: All tags must use Title Case (e.g., Expense Reports, Quick Expenses)\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]*$\"\n\n  concur-path-kebab-case:\n    description: >-\n     \
  \ SAP Concur API paths use lowercase kebab-case for multi-word resource names\n      (e.g., /expense/quickexpenses, /expense/receiptimages)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  concur-response-200-has-schema:\n    description: All 200 responses must have a response schema defined\n    severity: warn\n    given: \"$.paths[*][get,post].responses['200']\"\n    then:\n      field: content\n      function: defined\n\n  concur-pagination-limit-param:\n    description: >-\n      Collection endpoints (GET returning arrays) should support limit parameter\n      for pagination (max 100 per SAP Concur convention)\n    severity: hint\n    given: \"$.paths[*].get.parameters[?(@.name=='limit')]\"\n    then:\n      field: schema.maximum\n      function: defined\n\n  concur-pagination-offset-param:\n    description: >-\n      Collection endpoints should support offset parameter for cursor-based\n\
  \      pagination using the NextPage URL pattern\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            parameters:\n              type: array\n\n  concur-currency-code-format:\n    description: >-\n      Currency code fields must be ISO 4217 three-letter uppercase codes.\n      SAP Concur uses CurrencyCode and TransactionCurrencyCode naming.\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@property.match(/CurrencyCode$/))]\"\n    then:\n      field: pattern\n      function: defined\n\n  concur-id-field-type-string:\n    description: >-\n      SAP Concur uses string identifiers (hex GUIDs) for all resource IDs.\n      ID fields must be typed as string, not integer.\n    severity: error\n    given: \"$.components.schemas[*].properties.ID\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n\
  \          - string\n\n  concur-report-id-references:\n    description: >-\n      Expense entry endpoints require reportID as a query parameter when\n      listing entries. The ReportID parameter enables server-side filtering.\n    severity: hint\n    given: \"$.paths['/expense/entries'].get.parameters[?(@.name=='reportID')]\"\n    then:\n      field: required\n      function: truthy\n\n  concur-delete-returns-204:\n    description: >-\n      DELETE operations in SAP Concur APIs return 204 No Content on success\n      (not 200). Ensure DELETE responses use 204.\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: defined\n\n  concur-put-returns-204:\n    description: >-\n      PUT update operations in SAP Concur APIs return 204 No Content on success.\n      The full updated resource is retrieved via a subsequent GET.\n    severity: warn\n    given: \"$.paths[*].put.responses\"\n    then:\n      field: \"204\"\n      function:\
  \ defined\n\n  concur-post-create-returns-200:\n    description: >-\n      POST create operations return 200 with an ID response body rather than 201.\n      This follows SAP Concur v3 API conventions.\n    severity: info\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  concur-oauth2-security-defined:\n    description: >-\n      SAP Concur APIs require OAuth 2.0 authentication. All operations should\n      reference the OAuth2 security scheme.\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: OAuth2\n      function: defined\n\n  concur-entry-id-path-param:\n    description: >-\n      Path parameters for resource IDs should be named 'id' (lowercase)\n      following SAP Concur conventions.\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - id\n\n  concur-date-fields-iso8601:\n\
  \    description: >-\n      Date fields should use ISO 8601 format. Transaction dates use date format,\n      datetime fields use date-time format.\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@property.match(/Date$/))]\"\n    then:\n      field: format\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-concur-expense/refs/heads/main/rules/sap-concur-expense-rules.yml
tags:
- Expense Management
- Financial Management
- Receipts
- Reimbursement
- Reporting
- SAP
- Travel
- Spectral
- Linting
- API Governance
---
