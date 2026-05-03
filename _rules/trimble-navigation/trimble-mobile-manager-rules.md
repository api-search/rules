---
api_specs:
- filename: trimble-mobile-manager-openapi.yml
  format: yaml
  label: Trimble Mobile Manager API
  slug: trimble-mobile-manager
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trimble-navigation/refs/heads/main/openapi/trimble-mobile-manager-openapi.yml
categories:
- trimble
description: Spectral linting rules defining API design standards and conventions for Trimble Navigation.
layout: rules
name: Trimble Navigation API Rules
provider_name: Trimble Navigation
provider_slug: trimble-navigation
rule_count: 8
rules:
- description: All operations must have a camelCase operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: trimble-nav-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: trimble-nav-operation-id-camel-case
  severity: warn
- description: All API paths must use versioned prefix
  given: $.paths[*]~
  name: trimble-nav-versioned-path
  severity: warn
- description: All operations must define a 200 success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: trimble-nav-response-200-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: trimble-nav-operation-tags-required
  severity: warn
- description: API must use basic auth with computed access code
  given: $.components.securitySchemes[*]
  name: trimble-nav-basic-auth
  severity: warn
- description: Latitude and longitude must use double precision
  given: $.components.schemas[*].properties[?(@property == 'latitude' || @property == 'longitude')]
  name: trimble-nav-coordinate-precision
  severity: warn
- description: Path parameters must be required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: trimble-nav-path-params-required
  severity: error
rules_file: rules/trimble-mobile-manager-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trimble-navigation/refs/heads/main/rules/trimble-mobile-manager-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: trimble-mobile-manager-rules
source_filename: trimble-mobile-manager-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All operations must have operationId\n  trimble-nav-operation-id-required:\n    description: All operations must have a camelCase operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Operation IDs must use camelCase\n  trimble-nav-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # API paths must be versioned\n  trimble-nav-versioned-path:\n    description: All API paths must use versioned prefix\n    message: \"Path '{{value}}' must start with /api/v1/ or /api/v2/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[12]/\"\n\n  # All operations must define a 200 response\n  trimble-nav-response-200-required:\n    description: All operations must define a 200 success response\n    message: \"Operation is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # All operations must have tags\n  trimble-nav-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # Basic auth must be used\n  trimble-nav-basic-auth:\n    description: API must use basic auth with computed access code\n    message: \"\
  Security scheme must use HTTP basic authentication\"\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              const: http\n            scheme:\n              const: basic\n\n  # Coordinate fields must use double precision\n  trimble-nav-coordinate-precision:\n    description: Latitude and longitude must use double precision\n    message: \"Coordinate field should use format: double for sub-centimeter precision\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@property == 'latitude' || @property == 'longitude')]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - double\n\n  # Path parameters must be required\n  trimble-nav-path-params-required:\n    description: Path parameters must be required\n    message: \"Path parameter must have\
  \ required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trimble-navigation/refs/heads/main/rules/trimble-mobile-manager-rules.yml
tags:
- GPS
- GNSS
- Positioning
- Navigation
- Surveying
- Geospatial
- Construction
- Spectral
- Linting
- API Governance
---
