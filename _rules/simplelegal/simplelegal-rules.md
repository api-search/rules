---
api_specs:
- filename: simplelegal-openapi.yml
  format: yaml
  label: SimpleLegal API
  slug: simplelegal
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/simplelegal/refs/heads/main/openapi/simplelegal-openapi.yml
categories:
- simplelegal
description: Spectral linting rules defining API design standards and conventions for SimpleLegal.
layout: rules
name: SimpleLegal API Rules
provider_name: SimpleLegal
provider_slug: simplelegal
rule_count: 8
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: simplelegal-summary-title-case
  severity: warn
- description: OperationIds must use kebab-case naming.
  given: $.paths[*][*].operationId
  name: simplelegal-operationid-kebab-case
  severity: warn
- description: Collection GET endpoints should support page and page_size parameters.
  given: $.paths[?(!@property.match(/{.*}/))].get.parameters[*].name
  name: simplelegal-pagination-params
  severity: info
- description: API must use HTTP Basic authentication.
  given: $.components.securitySchemes[*].scheme
  name: simplelegal-basic-auth
  severity: warn
- description: Update operations should prefer PATCH over PUT.
  given: $.paths[*].put.operationId
  name: simplelegal-patch-update
  severity: info
- description: All responses should return application/json.
  given: $.paths[*][*].responses[?(@property >= '200')].content
  name: simplelegal-json-responses
  severity: warn
- description: Operations should document authentication and not-found error responses.
  given: $.paths[*][*].responses
  name: simplelegal-error-responses
  severity: info
- description: All paths and operations must have descriptions.
  given:
  - $.paths[*][*]
  - $.info
  name: simplelegal-descriptions-required
  severity: warn
rules_file: rules/simplelegal-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/simplelegal/refs/heads/main/rules/simplelegal-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 3
  warn: 5
slug: simplelegal-rules
source_filename: simplelegal-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  simplelegal-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  simplelegal-operationid-kebab-case:\n    description: OperationIds must use kebab-case naming.\n    message: \"OperationId '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9]*(-[a-z0-9]+)*$\"\n\n  simplelegal-pagination-params:\n    description: Collection GET endpoints should support page and page_size parameters.\n    message: \"Collection endpoint should support pagination parameters.\"\n    severity: info\n    given: \"$.paths[?(!@property.match(/{.*}/))].get.parameters[*].name\"\
  \n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - page_size\n          - status\n          - matter_id\n          - vendor_id\n          - type\n          - active\n\n  simplelegal-basic-auth:\n    description: API must use HTTP Basic authentication.\n    message: \"API should use HTTP Basic authentication.\"\n    severity: warn\n    given: \"$.components.securitySchemes[*].scheme\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - basic\n\n  simplelegal-patch-update:\n    description: Update operations should prefer PATCH over PUT.\n    message: \"Update operations should use PATCH for partial updates.\"\n    severity: info\n    given: \"$.paths[*].put.operationId\"\n    then:\n      function: falsy\n\n  simplelegal-json-responses:\n    description: All responses should return application/json.\n    message: \"Response should include application/json content type.\"\n    severity:\
  \ warn\n    given: \"$.paths[*][*].responses[?(@property >= '200')].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"application/json\"\n\n  simplelegal-error-responses:\n    description: Operations should document authentication and not-found error responses.\n    message: \"Operation should document error responses (401, 404).\"\n    severity: info\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: truthy\n\n  simplelegal-descriptions-required:\n    description: All paths and operations must have descriptions.\n    message: \"{{property}} is missing a description.\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.info\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/simplelegal/refs/heads/main/rules/simplelegal-rules.yml
tags:
- eBilling
- Enterprise Legal Management
- Legal Operations
- Legal Spend Management
- Matter Management
- Vendor Management
- Spectral
- Linting
- API Governance
---
