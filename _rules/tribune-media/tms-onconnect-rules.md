---
api_specs:
- filename: tms-onconnect-openapi.yml
  format: yaml
  label: TMS OnConnect API
  slug: tms-onconnect
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tribune-media/refs/heads/main/openapi/tms-onconnect-openapi.yml
categories:
- tms
description: Spectral linting rules defining API design standards and conventions for Tribune Media.
layout: rules
name: Tribune Media API Rules
provider_name: Tribune Media
provider_slug: tribune-media
rule_count: 12
rules:
- description: All TMS OnConnect operations must include the api_key query parameter
  given: $.paths[*][get,post,put,delete].parameters
  name: tms-api-key-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete]
  name: tms-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,delete].operationId
  name: tms-operation-id-camel-case
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,delete]
  name: tms-operation-tags-required
  severity: warn
- description: DateTime parameters must specify format as date-time
  given: $.paths[*][get,post,put,delete].parameters[?(@.name =~ /DateTime$/)]
  name: tms-datetime-parameter-format
  severity: warn
- description: Date parameters must specify format as date
  given: $.paths[*][get,post,put,delete].parameters[?(@.name =~ /Date$/)]
  name: tms-date-parameter-format
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,delete].responses
  name: tms-response-200-required
  severity: error
- description: Path IDs in curly braces must use camelCase
  given: $.paths[*]~
  name: tms-path-ids-kebab-case
  severity: hint
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: tms-schema-property-descriptions
  severity: hint
- description: imageSize parameters must use standard TMS size values
  given: $.paths[*][get].parameters[?(@.name == 'imageSize')]
  name: tms-image-size-enum
  severity: hint
- description: Lineup sub-resource paths must have a lineupId path parameter
  given: $.paths['/v1.1/lineups/{lineupId}'][*].parameters
  name: tms-lineup-path-parameter
  severity: warn
- description: Path parameters must be required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: tms-path-params-required
  severity: error
rules_file: rules/tms-onconnect-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tribune-media/refs/heads/main/rules/tms-onconnect-rules.yml
severity_counts:
  error: 4
  hint: 3
  info: 0
  warn: 5
slug: tms-onconnect-rules
source_filename: tms-onconnect-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All operations must use API key authentication via query parameter\n  tms-api-key-required:\n    description: All TMS OnConnect operations must include the api_key query parameter\n    message: \"Operation '{{operationId}}' is missing the required api_key query parameter\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                type: string\n                const: api_key\n              in:\n                type: string\n                const: query\n\n  # All operations must have operationId\n  tms-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n\
  \      field: operationId\n      function: truthy\n\n  # operationIds must use camelCase\n  tms-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have at least one tag\n  tms-operation-tags-required:\n    description: All operations must be tagged\n    message: \"Operation '{{operationId}}' must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # Date/time parameters must use ISO 8601 format\n  tms-datetime-parameter-format:\n    description: DateTime parameters must specify format as date-time\n    message:\
  \ \"Parameter '{{value}}' ending in 'DateTime' must have format: date-time\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].parameters[?(@.name =~ /DateTime$/)]\"\n    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  # Date parameters must use ISO 8601 date format\n  tms-date-parameter-format:\n    description: Date parameters must specify format as date\n    message: \"Parameter ending in 'Date' must have format: date\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].parameters[?(@.name =~ /Date$/)]\"\n    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n\n  # Responses must include 200 and 401 status codes\n  tms-response-200-required:\n    description: All operations must define a 200 response\n    message: \"Operation is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete].responses\"\
  \n    then:\n      field: \"200\"\n      function: truthy\n\n  # Path parameters must match the path template\n  tms-path-ids-kebab-case:\n    description: Path IDs in curly braces must use camelCase\n    message: \"Path parameter '{{value}}' should use camelCase\"\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[12])?(/[a-z][a-zA-Z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9_]*\\\\})*$\"\n\n  # All schemas must have descriptions\n  tms-schema-property-descriptions:\n    description: Schema properties should have descriptions\n    message: \"Schema property '{{path}}' is missing a description\"\n    severity: hint\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # imageSize enum values must be standard\n  tms-image-size-enum:\n    description: imageSize parameters must use standard TMS size values\n    message: \"imageSize parameter should enumerate\
  \ valid TMS image sizes\"\n    severity: hint\n    given: \"$.paths[*][get].parameters[?(@.name == 'imageSize')]\"\n    then:\n      field: schema\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              const: string\n\n  # Lineups endpoints must include lineupId\n  tms-lineup-path-parameter:\n    description: Lineup sub-resource paths must have a lineupId path parameter\n    message: \"Lineup sub-resource '{{path}}' must define the lineupId path parameter\"\n    severity: warn\n    given: \"$.paths['/v1.1/lineups/{lineupId}'][*].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: lineupId\n              in:\n                const: path\n\n  # All path parameters must be marked required: true\n  tms-path-params-required:\n\
  \    description: Path parameters must be required\n    message: \"Path parameter '{{value}}' must be marked as required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tribune-media/refs/heads/main/rules/tms-onconnect-rules.yml
tags:
- Media
- Entertainment
- Broadcasting
- Television
- Movies
- Sports
- Celebrity
- Spectral
- Linting
- API Governance
---
