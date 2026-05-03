---
api_specs:
- filename: terrain-openapi.yml
  format: yaml
  label: Terrain API
  slug: terrain-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/terrain-discovery-environment-api/refs/heads/main/openapi/terrain-openapi.yml
categories:
- terrain
description: Spectral linting rules defining API design standards and conventions for Terrain Discovery Environment API.
layout: rules
name: Terrain Discovery Environment API API Rules
provider_name: Terrain Discovery Environment API
provider_slug: terrain-discovery-environment-api
rule_count: 8
rules:
- description: All operations must have operationId defined
  given: $.paths.*[get,post,put,patch,delete]
  name: terrain-operation-ids-present
  severity: error
- description: Operation IDs should use PascalCase
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: terrain-operation-id-pascal-case
  severity: warn
- description: Authenticated endpoints should be under /secured prefix
  given: $.paths
  name: terrain-secured-paths
  severity: info
- description: Each operation should have at least one tag
  given: $.paths.*[get,post,put,patch,delete]
  name: terrain-tags-required
  severity: warn
- description: Parameters should have descriptions
  given: $.paths..parameters[*]
  name: terrain-parameter-descriptions
  severity: warn
- description: Endpoints should return application/json responses
  given: $.paths.*[get,post,put,patch,delete].responses.*.content
  name: terrain-json-responses
  severity: warn
- description: Terrain uses JWT bearer token or X-Iplant-De-Jwt header authentication
  given: $.components.securitySchemes.*
  name: terrain-jwt-auth
  severity: info
- description: Path parameter names should use kebab-case
  given: $.paths..parameters[?(@.in == 'path')].name
  name: terrain-kebab-path-params
  severity: warn
rules_file: rules/terrain-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/terrain-discovery-environment-api/refs/heads/main/rules/terrain-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 5
slug: terrain-rules
source_filename: terrain-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  terrain-operation-ids-present:\n    description: All operations must have operationId defined\n    message: \"Operation at {{path}} is missing operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  terrain-operation-id-pascal-case:\n    description: Operation IDs should use PascalCase\n    message: \"Operation ID '{{value}}' should use PascalCase\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]+$\"\n\n  terrain-secured-paths:\n    description: Authenticated endpoints should be under /secured prefix\n    message: \"Authenticated endpoints should use /secured path prefix\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \n  terrain-tags-required:\n    description: Each operation should have at least one tag\n    message: \"Operation at {{path}} should have at least one tag\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  terrain-parameter-descriptions:\n    description: Parameters should have descriptions\n    message: \"Parameter is missing a description\"\n    severity: warn\n    given: \"$.paths..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  terrain-json-responses:\n    description: Endpoints should return application/json responses\n    message: \"Response should use application/json content type\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].responses.*.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            \"application/json\":\n              type: object\n\n  terrain-jwt-auth:\n\
  \    description: Terrain uses JWT bearer token or X-Iplant-De-Jwt header authentication\n    message: \"Security schemes should use bearer JWT or apiKey header\"\n    severity: info\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  const: bearer\n            - properties:\n                type:\n                  const: apiKey\n                in:\n                  const: header\n\n  terrain-kebab-path-params:\n    description: Path parameter names should use kebab-case\n    message: \"Path parameter '{{value}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths..parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9-]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/terrain-discovery-environment-api/refs/heads/main/rules/terrain-rules.yml
tags:
- Bioinformatics
- Data Science
- Life Sciences
- Filesystem
- Cloud Computing
- Open Source
- Spectral
- Linting
- API Governance
---
