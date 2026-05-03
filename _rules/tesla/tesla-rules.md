---
api_specs:
- filename: tesla-openapi-original.yml
  format: yaml
  label: Tesla Fleet API
  slug: fleet-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tesla/refs/heads/main/openapi/tesla-openapi-original.yml
- filename: tesla-openapi-original.yml
  format: yaml
  label: Tesla Owner API
  slug: owner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tesla/refs/heads/main/openapi/tesla-openapi-original.yml
categories:
- tesla
description: Spectral linting rules defining API design standards and conventions for Tesla.
layout: rules
name: Tesla API Rules
provider_name: Tesla
provider_slug: tesla
rule_count: 8
rules:
- description: All operations must have operationId defined
  given: $.paths.*[get,post,put,patch,delete]
  name: tesla-operation-ids-present
  severity: error
- description: Operation IDs should use PascalCase
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: tesla-operation-id-pascal-case
  severity: warn
- description: Tesla API summaries should start with the provider name "Tesla"
  given: $.paths.*[get,post,put,patch,delete].summary
  name: tesla-summaries-start-with-provider
  severity: info
- description: Each operation should have at least one tag
  given: $.paths.*[get,post,put,patch,delete]
  name: tesla-tags-required
  severity: warn
- description: Tesla API uses OAuth2 bearer token authentication
  given: $.components.securitySchemes.*
  name: tesla-bearer-auth
  severity: warn
- description: Vehicle endpoints should use vehicle_id path parameter
  given: $.paths./api/1/vehicles/*
  name: tesla-vehicle-id-path-param
  severity: info
- description: Operations should define a 200 response
  given: $.paths.*[get,post]
  name: tesla-response-200
  severity: warn
- description: Path parameters should have descriptions
  given: $.paths..parameters[?(@.in == 'path')]
  name: tesla-parameter-descriptions
  severity: warn
rules_file: rules/tesla-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tesla/refs/heads/main/rules/tesla-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 5
slug: tesla-rules
source_filename: tesla-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tesla-operation-ids-present:\n    description: All operations must have operationId defined\n    message: \"Operation at {{path}} is missing operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tesla-operation-id-pascal-case:\n    description: Operation IDs should use PascalCase\n    message: \"Operation ID '{{value}}' should use PascalCase\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]+$\"\n\n  tesla-summaries-start-with-provider:\n    description: Tesla API summaries should start with the provider name \"Tesla\"\n    message: \"Summary '{{value}}' should start with 'Tesla '\"\n    severity: info\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^Tesla \"\n\n  tesla-tags-required:\n    description: Each operation should have at least one tag\n    message: \"Operation at {{path}} should have at least one tag\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  tesla-bearer-auth:\n    description: Tesla API uses OAuth2 bearer token authentication\n    message: \"Security should use bearer token\"\n    severity: warn\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  const: bearer\n            - properties:\n                type:\n                  const: oauth2\n\n  tesla-vehicle-id-path-param:\n    description: Vehicle endpoints should use vehicle_id path parameter\n    message: \"Vehicle path should\
  \ use {vehicle_id} parameter\"\n    severity: info\n    given: \"$.paths./api/1/vehicles/*\"\n    then:\n      function: truthy\n\n  tesla-response-200:\n    description: Operations should define a 200 response\n    message: \"Operation should define a 200 OK response\"\n    severity: warn\n    given: \"$.paths.*[get,post]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n              required: [\"200\"]\n\n  tesla-parameter-descriptions:\n    description: Path parameters should have descriptions\n    message: \"Path parameter is missing a description\"\n    severity: warn\n    given: \"$.paths..parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tesla/refs/heads/main/rules/tesla-rules.yml
tags:
- Automobiles
- Cars
- Vehicles
- Electric Vehicles
- Energy
- Clean Energy
- IoT
- Spectral
- Linting
- API Governance
---
