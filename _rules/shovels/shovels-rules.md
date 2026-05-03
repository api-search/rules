---
api_specs:
- filename: shovels-openapi.yml
  format: yaml
  label: Shovels API
  slug: shovels-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shovels/refs/heads/main/openapi/shovels-openapi.yml
categories:
- shovels
description: Spectral linting rules defining API design standards and conventions for Shovels.
layout: rules
name: Shovels API Rules
provider_name: Shovels
provider_slug: shovels
rule_count: 10
rules:
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: shovels-operation-tags
  severity: error
- description: All operations must have a summary in Title Case
  given: $.paths[*][*]
  name: shovels-operation-summary
  severity: error
- description: API must use X-API-Key header authentication
  given: $.components.securitySchemes[*]
  name: shovels-api-key-auth
  severity: error
- description: Geographic search endpoints must include geo_id parameter
  given: $.paths[*].get.parameters[?(@.name == 'geo_id')]
  name: shovels-geo-id-parameter
  severity: warn
- description: List endpoints should support cursor-based pagination
  given: $.paths[*].get.parameters[?(@.name == 'cursor')]
  name: shovels-cursor-pagination
  severity: warn
- description: Date parameters must use YYYY-MM-DD format
  given: $.paths[*].get.parameters[?(@.schema.format == 'date')]
  name: shovels-date-format
  severity: warn
- description: All GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: shovels-response-200
  severity: error
- description: Operations with required parameters should document 422 validation errors
  given: $.paths[*].get.responses
  name: shovels-response-422
  severity: warn
- description: List response schemas should have items array property
  given: $.components.schemas[*Response]
  name: shovels-items-schema
  severity: error
- description: Geographic schemas should include geo_id field
  given: $.components.schemas[*]
  name: shovels-geo-id-field
  severity: warn
rules_file: rules/shovels-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shovels/refs/heads/main/rules/shovels-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: shovels-rules
source_filename: shovels-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shovels-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operation '{{property}}' must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  shovels-operation-summary:\n    description: All operations must have a summary in Title Case\n    message: \"Operation must have a summary\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: summary\n      function: truthy\n\n  shovels-api-key-auth:\n    description: API must use X-API-Key header authentication\n    message: \"Security scheme must be apiKey in header named X-API-Key\"\n    given: \"$.components.securitySchemes[*]\"\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              enum: [apiKey]\n            in:\n              enum: [header]\n          \
  \  name:\n              enum: [X-API-Key]\n\n  shovels-geo-id-parameter:\n    description: Geographic search endpoints must include geo_id parameter\n    message: \"Search endpoints for geographic data should document geo_id parameter\"\n    given: \"$.paths[*].get.parameters[?(@.name == 'geo_id')]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  shovels-cursor-pagination:\n    description: List endpoints should support cursor-based pagination\n    message: \"List endpoints should have cursor pagination parameter\"\n    given: \"$.paths[*].get.parameters[?(@.name == 'cursor')]\"\n    severity: warn\n    then:\n      field: schema\n      function: truthy\n\n  shovels-date-format:\n    description: Date parameters must use YYYY-MM-DD format\n    message: \"Date parameters must specify format: date\"\n    given: \"$.paths[*].get.parameters[?(@.schema.format == 'date')]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\
  \n  shovels-response-200:\n    description: All GET operations must have a 200 response\n    message: \"GET operation must define a 200 response\"\n    given: \"$.paths[*].get.responses\"\n    severity: error\n    then:\n      field: \"200\"\n      function: truthy\n\n  shovels-response-422:\n    description: Operations with required parameters should document 422 validation errors\n    message: \"Operations should document 422 validation error responses\"\n    given: \"$.paths[*].get.responses\"\n    severity: warn\n    then:\n      field: \"422\"\n      function: defined\n\n  shovels-items-schema:\n    description: List response schemas should have items array property\n    message: \"List response must include items array\"\n    given: \"$.components.schemas[*Response]\"\n    severity: error\n    then:\n      field: properties.items\n      function: truthy\n\n  shovels-geo-id-field:\n    description: Geographic schemas should include geo_id field\n    message: \"Geographic schemas should\
  \ include geo_id identifier field\"\n    given: \"$.components.schemas[*]\"\n    severity: warn\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shovels/refs/heads/main/rules/shovels-rules.yml
tags:
- Construction
- Building Permits
- Contractors
- Real Estate
- Property Data
- Market Intelligence
- Spectral
- Linting
- API Governance
---
