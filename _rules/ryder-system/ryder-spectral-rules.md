---
api_specs:
- filename: ryder-fleet-management-api-openapi.yml
  format: yaml
  label: Ryder Fleet Management API
  slug: fleet-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ryder-system/refs/heads/main/openapi/ryder-fleet-management-api-openapi.yml
- filename: ryder-carrier-api-openapi.yml
  format: yaml
  label: Ryder Carrier API
  slug: carrier-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ryder-system/refs/heads/main/openapi/ryder-carrier-api-openapi.yml
- filename: ryder-tm-shipment-api-openapi.yml
  format: yaml
  label: Ryder TM Shipment Management API
  slug: tm-shipment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ryder-system/refs/heads/main/openapi/ryder-tm-shipment-api-openapi.yml
categories:
- ryder
description: Spectral linting rules defining API design standards and conventions for Ryder System.
layout: rules
name: Ryder System API Rules
provider_name: Ryder System
provider_slug: ryder-system
rule_count: 7
rules:
- description: Ryder APIs use API key authentication via Ocp-Apim-Subscription-Key header
  given: $.components.securitySchemes
  name: ryder-api-key-auth
  severity: error
- description: All Ryder operationIds should use camelCase
  given: $.paths[*][*].operationId
  name: ryder-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: ryder-tags-title-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ryder-summaries-title-case
  severity: warn
- description: All operations must have a 200 or 201 success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: ryder-response-200-required
  severity: error
- description: List operations should support page/pageSize pagination
  given: $.paths[*].get
  name: ryder-pagination-page-params
  severity: info
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: ryder-path-params-required
  severity: error
rules_file: rules/ryder-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ryder-system/refs/heads/main/rules/ryder-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: ryder-spectral-rules
source_filename: ryder-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ryder-api-key-auth:\n    description: Ryder APIs use API key authentication via Ocp-Apim-Subscription-Key header\n    message: \"API must define Ocp-Apim-Subscription-Key apiKey security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  ryder-operation-id-camel-case:\n    description: All Ryder operationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase naming\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ryder-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  ryder-summaries-title-case:\n \
  \   description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  ryder-response-200-required:\n    description: All operations must have a 200 or 201 success response\n    message: \"Operation '{{description}}' is missing a success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  ryder-pagination-page-params:\n    description: List operations should support page/pageSize pagination\n    message: \"List operation should support page and pageSize parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n\
  \      function: truthy\n\n  ryder-path-params-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter '{{value}}' must be marked as required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ryder-system/refs/heads/main/rules/ryder-spectral-rules.yml
tags:
- Fleet Management
- Logistics
- Supply Chain
- Transportation
- Trucking
- Spectral
- Linting
- API Governance
---
