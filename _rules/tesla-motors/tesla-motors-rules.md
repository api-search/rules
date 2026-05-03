---
api_specs:
- filename: tesla-motors-owner-openapi.yml
  format: yaml
  label: Tesla Owner API
  slug: owner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tesla-motors/refs/heads/main/openapi/tesla-motors-owner-openapi.yml
categories:
- tesla
description: Spectral linting rules defining API design standards and conventions for Tesla Motors.
layout: rules
name: Tesla Motors API Rules
provider_name: Tesla Motors
provider_slug: tesla-motors
rule_count: 7
rules:
- description: All operations must have operationId defined
  given: $.paths.*[get,post,put,patch,delete]
  name: tesla-operation-ids-present
  severity: error
- description: Operation IDs should use PascalCase
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: tesla-operation-id-pascal-case
  severity: warn
- description: Tesla API uses bearer token authentication
  given: $.components.securitySchemes.*
  name: tesla-bearer-auth
  severity: warn
- description: Each operation should have at least one tag
  given: $.paths.*[get,post,put,patch,delete]
  name: tesla-tags-required
  severity: warn
- description: Vehicle endpoints should use vehicle_id path parameter
  given: $.paths./api/1/vehicles/*
  name: tesla-vehicle-id-path-param
  severity: info
- description: Operation summaries should use Title Case
  given: $.paths.*[get,post,put,patch,delete].summary
  name: tesla-summaries-title-case
  severity: warn
- description: Operations should define a 200 response
  given: $.paths.*[get,post]
  name: tesla-response-200
  severity: warn
rules_file: rules/tesla-motors-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tesla-motors/refs/heads/main/rules/tesla-motors-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 5
slug: tesla-motors-rules
source_filename: tesla-motors-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tesla-operation-ids-present:\n    description: All operations must have operationId defined\n    message: \"Operation at {{path}} is missing operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tesla-operation-id-pascal-case:\n    description: Operation IDs should use PascalCase\n    message: \"Operation ID '{{value}}' should use PascalCase\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]+$\"\n\n  tesla-bearer-auth:\n    description: Tesla API uses bearer token authentication\n    message: \"Security scheme should use bearer token\"\n    severity: warn\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n\
  \            type:\n              const: http\n            scheme:\n              const: bearer\n\n  tesla-tags-required:\n    description: Each operation should have at least one tag\n    message: \"Operation at {{path}} should have at least one tag\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  tesla-vehicle-id-path-param:\n    description: Vehicle endpoints should use vehicle_id path parameter\n    message: \"Vehicle path should use {vehicle_id} parameter\"\n    severity: info\n    given: \"$.paths./api/1/vehicles/*\"\n    then:\n      function: truthy\n\n  tesla-summaries-title-case:\n    description: Operation summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  tesla-response-200:\n   \
  \ description: Operations should define a 200 response\n    message: \"Operation should define a 200 OK response\"\n    severity: warn\n    given: \"$.paths.*[get,post]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n              required: [\"200\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tesla-motors/refs/heads/main/rules/tesla-motors-rules.yml
tags:
- Automobiles
- Electric Vehicles
- Cars
- Smart Vehicles
- IoT
- Spectral
- Linting
- API Governance
---
