---
api_specs:
- filename: toyota-telematics-openapi.yml
  format: yaml
  label: Toyota Telematics API
  slug: toyota-telematics
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toyota/refs/heads/main/openapi/toyota-telematics-openapi.yml
- filename: toyota-connected-services-openapi.yml
  format: yaml
  label: Toyota Connected Services API
  slug: toyota-connected-services
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toyota/refs/heads/main/openapi/toyota-connected-services-openapi.yml
categories:
- toyota
description: Spectral linting rules defining API design standards and conventions for Toyota.
layout: rules
name: Toyota API Rules
provider_name: Toyota
provider_slug: toyota
rule_count: 9
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: toyota-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: toyota-operation-summary-title-case
  severity: warn
- description: API paths must use kebab-case
  given: $.paths[*]~
  name: toyota-paths-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: toyota-must-have-tags
  severity: error
- description: VIN path parameters should have proper length constraints
  given: $.paths[*][*].parameters[?(@.name == 'vin' && @.in == 'path')]
  name: toyota-vin-path-parameter
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: toyota-must-have-200-or-201
  severity: error
- description: List operations should support pagination parameters
  given: $.paths[*][get][?(@.operationId =~ /^list/)]
  name: toyota-pagination-on-list-operations
  severity: warn
- description: All vehicle endpoints must require authentication
  given: $.paths[/vehicles*][get,post,put,patch,delete]
  name: toyota-vehicle-endpoints-auth
  severity: error
- description: Latitude and longitude fields should use double format
  given: $.components.schemas[*].properties[latitude,longitude]
  name: toyota-coordinates-format
  severity: warn
rules_file: rules/toyota-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toyota/refs/heads/main/rules/toyota-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 6
slug: toyota-spectral-rules
source_filename: toyota-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  toyota-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  toyota-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  toyota-paths-kebab-case:\n    description: API paths must use kebab-case\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-]+|/\\\\{[a-zA-Z0-9]+\\\\})*$\"\n\n  toyota-must-have-tags:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  toyota-vin-path-parameter:\n\
  \    description: VIN path parameters should have proper length constraints\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'vin' && @.in == 'path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            schema:\n              properties:\n                minLength:\n                  enum: [17]\n                maxLength:\n                  enum: [17]\n\n  toyota-must-have-200-or-201:\n    description: All operations must define a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  toyota-pagination-on-list-operations:\n    description: List operations should support pagination parameters\n    severity: warn\n    given: \"$.paths[*][get][?(@.operationId =~ /^list/)]\"\n    then:\n      field:\
  \ parameters\n      function: truthy\n\n  toyota-vehicle-endpoints-auth:\n    description: All vehicle endpoints must require authentication\n    given: \"$.paths[/vehicles*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: security\n      function: truthy\n\n  toyota-coordinates-format:\n    description: Latitude and longitude fields should use double format\n    severity: warn\n    given: \"$.components.schemas[*].properties[latitude,longitude]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            format:\n              enum: [\"double\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toyota/refs/heads/main/rules/toyota-spectral-rules.yml
tags:
- Automobiles
- Cars
- Vehicles
- Connected Car
- Telematics
- Fleet Management
- Electric Vehicles
- Spectral
- Linting
- API Governance
---
