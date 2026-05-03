---
api_specs:
- filename: schematic-openapi.yml
  format: yaml
  label: Schematic API
  slug: schematic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/schematic/refs/heads/main/openapi/schematic-openapi.yml
categories:
- schematic
description: Spectral linting rules defining API design standards and conventions for Schematic.
layout: rules
name: Schematic API Rules
provider_name: Schematic
provider_slug: schematic
rule_count: 11
rules:
- description: Operation IDs should use camelCase naming consistent with Schematic API conventions.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: schematic-operation-ids-camel-case
  severity: warn
- description: Operation summaries should use Title Case for consistency.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: schematic-summary-title-case
  severity: warn
- description: Operations with 'list' in the operationId should return an array or paginated response object.
  given: $.paths[*].get
  name: schematic-list-operations-return-arrays
  severity: warn
- description: Schematic APIs expose count endpoints alongside list endpoints. Count endpoints should follow the /count suffix pattern.
  given: $.paths
  name: schematic-count-endpoints-exist
  severity: info
- description: Schematic API responses wrap data in a 'data' field with a ResponseData schema. Response schemas should follow the *ResponseData naming convention.
  given: $.components.schemas
  name: schematic-response-data-wrapper
  severity: warn
- description: Schematic API uses X-Schematic-Api-Key header for authentication. All operations should be secured with ApiKeyAuth.
  given: $.components.securitySchemes.ApiKeyAuth
  name: schematic-api-key-auth-header
  severity: error
- description: All error responses (4xx, 5xx) should reference the ApiError schema.
  given: $.paths[*][*].responses[4xx,5xx]
  name: schematic-error-response-schema
  severity: warn
- description: Schematic upsert operations use POST method. Operations named 'upsert*' should use POST.
  given: $.paths[*].post.operationId
  name: schematic-upsert-operations-use-post
  severity: warn
- description: Delete operations should target resources by ID path parameter.
  given: $.paths[*].delete
  name: schematic-delete-operations-by-id
  severity: warn
- description: Flag check operations support both single-key (/flags/{key}/check) and bulk (/flags/check-bulk) patterns.
  given: $.paths['/flags/check-bulk']
  name: schematic-bulk-check-operations
  severity: info
- description: List operations should support pagination via limit and offset parameters.
  given: $.paths[*].get.parameters[*].name
  name: schematic-pagination-params
  severity: warn
rules_file: rules/schematic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/schematic/refs/heads/main/rules/schematic-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 8
slug: schematic-rules
source_filename: schematic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Schematic API uses consistent resource naming patterns\n  schematic-operation-ids-camel-case:\n    description: Operation IDs should use camelCase naming consistent with Schematic API conventions.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schematic-summary-title-case:\n    description: Operation summaries should use Title Case for consistency.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  schematic-list-operations-return-arrays:\n    description: >-\n      Operations with 'list' in the operationId should return an array or\n      paginated response object.\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: truthy\n\n  schematic-count-endpoints-exist:\n\
  \    description: >-\n      Schematic APIs expose count endpoints alongside list endpoints.\n      Count endpoints should follow the /count suffix pattern.\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: truthy\n\n  schematic-response-data-wrapper:\n    description: >-\n      Schematic API responses wrap data in a 'data' field with a ResponseData\n      schema. Response schemas should follow the *ResponseData naming convention.\n    severity: warn\n    given: \"$.components.schemas\"\n    then:\n      function: truthy\n\n  schematic-api-key-auth-header:\n    description: >-\n      Schematic API uses X-Schematic-Api-Key header for authentication.\n      All operations should be secured with ApiKeyAuth.\n    severity: error\n    given: \"$.components.securitySchemes.ApiKeyAuth\"\n    then:\n      function: truthy\n\n  schematic-error-response-schema:\n    description: >-\n      All error responses (4xx, 5xx) should reference the ApiError schema.\n    severity: warn\n\
  \    given: \"$.paths[*][*].responses[4xx,5xx]\"\n    then:\n      function: truthy\n\n  schematic-upsert-operations-use-post:\n    description: >-\n      Schematic upsert operations use POST method. Operations named 'upsert*'\n      should use POST.\n    severity: warn\n    given: \"$.paths[*].post.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(get|list|count|delete)\"\n\n  schematic-delete-operations-by-id:\n    description: >-\n      Delete operations should target resources by ID path parameter.\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      function: truthy\n\n  schematic-bulk-check-operations:\n    description: >-\n      Flag check operations support both single-key (/flags/{key}/check) and\n      bulk (/flags/check-bulk) patterns.\n    severity: info\n    given: \"$.paths['/flags/check-bulk']\"\n    then:\n      function: truthy\n\n  schematic-pagination-params:\n    description: >-\n      List operations\
  \ should support pagination via limit and offset parameters.\n    severity: warn\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/schematic/refs/heads/main/rules/schematic-rules.yml
tags:
- Billing
- Entitlements
- Feature Flags
- Feature Management
- FinOps
- Metering
- Pricing
- SaaS
- Spectral
- Linting
- API Governance
---
