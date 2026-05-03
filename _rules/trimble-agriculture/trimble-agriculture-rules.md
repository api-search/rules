---
api_specs:
- filename: trimble-agriculture-openapi.yml
  format: yaml
  label: Trimble Agriculture Data API
  slug: trimble-agriculture-data
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trimble-agriculture/refs/heads/main/openapi/trimble-agriculture-openapi.yml
categories:
- trimble
description: Spectral linting rules defining API design standards and conventions for Trimble Agriculture.
layout: rules
name: Trimble Agriculture API Rules
provider_name: Trimble Agriculture
provider_slug: trimble-agriculture
rule_count: 11
rules:
- description: All operations must have a camelCase operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: trimble-ag-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: trimble-ag-operation-id-camel-case
  severity: warn
- description: All resource paths must be scoped under an organizationId
  given: $.paths[*]~
  name: trimble-ag-organization-context
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: trimble-ag-path-params-required
  severity: error
- description: ID parameters should specify uuid format
  given: $.paths[*][*].parameters[?(@.name =~ /Id$/)]
  name: trimble-ag-uuid-format
  severity: hint
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: trimble-ag-operation-tags-required
  severity: warn
- description: All operations must define a 200 success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: trimble-ag-response-200-required
  severity: error
- description: API must use bearer authentication
  given: $.components.securitySchemes[*]
  name: trimble-ag-bearer-auth
  severity: error
- description: Boundary and geometry fields should reference GeoJsonGeometry
  given: $.components.schemas[*].properties[?(@property == 'boundary' || @property == 'geometry')]
  name: trimble-ag-geojson-geometry
  severity: hint
- description: POST operations must have a request body
  given: $.paths[*].post
  name: trimble-ag-post-has-request-body
  severity: error
- description: Date-time parameters must specify format date-time
  given: $.paths[*][*].parameters[?(@.name =~ /Date$|Time$/)]
  name: trimble-ag-datetime-format
  severity: warn
rules_file: rules/trimble-agriculture-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trimble-agriculture/refs/heads/main/rules/trimble-agriculture-rules.yml
severity_counts:
  error: 5
  hint: 2
  info: 0
  warn: 4
slug: trimble-agriculture-rules
source_filename: trimble-agriculture-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All operations must have operationId\n  trimble-ag-operation-id-required:\n    description: All operations must have a camelCase operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Operations must use camelCase identifiers\n  trimble-ag-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Organization ID must be first path parameter for all resource paths\n  trimble-ag-organization-context:\n    description: All resource paths must be scoped under an organizationId\n    message: \"Path '{{value}}' should begin with\
  \ /organizations/{organizationId}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/organizations/\\\\{organizationId\\\\}\"\n\n  # Path parameters must be required\n  trimble-ag-path-params-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter must have required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  # IDs should use UUID format\n  trimble-ag-uuid-format:\n    description: ID parameters should specify uuid format\n    message: \"ID parameter '{{value}}' should have format: uuid\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.name =~ /Id$/)]\"\n    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - uuid\n\n  # All operations must have tags\n  trimble-ag-operation-tags-required:\n\
  \    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # All operations must define a 200 response\n  trimble-ag-response-200-required:\n    description: All operations must define a 200 success response\n    message: \"Operation is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # Bearer auth must be defined\n  trimble-ag-bearer-auth:\n    description: API must use bearer authentication\n    message: \"Security scheme must use type: http with scheme: bearer\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  # GeoJSON geometry should reference the GeoJsonGeometry schema\n  trimble-ag-geojson-geometry:\n    description: Boundary and geometry fields should reference GeoJsonGeometry\n    message: \"Geometry field should use GeoJSON format with type and coordinates\"\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@property == 'boundary' || @property == 'geometry')]\"\n    then:\n      function: truthy\n\n  # POST operations creating resources should document input schema\n  trimble-ag-post-has-request-body:\n    description: POST operations must have a request body\n    message: \"POST operation must define a requestBody\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Date/time parameters must use ISO 8601 format\n  trimble-ag-datetime-format:\n\
  \    description: Date-time parameters must specify format date-time\n    message: \"DateTime parameter should have format: date-time\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name =~ /Date$|Time$/)]\"\n    then:\n      field: schema.format\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trimble-agriculture/refs/heads/main/rules/trimble-agriculture-rules.yml
tags:
- Agriculture
- Farming
- IoT
- Precision Agriculture
- Field Management
- Prescriptions
- Telematics
- Spectral
- Linting
- API Governance
---
