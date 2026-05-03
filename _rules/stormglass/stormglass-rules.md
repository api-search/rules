---
api_specs:
- filename: stormglass-openapi.yml
  format: yaml
  label: Stormglass API
  slug: stormglass-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stormglass/refs/heads/main/openapi/stormglass-openapi.yml
categories:
- stormglass
description: Spectral linting rules defining API design standards and conventions for Stormglass.
layout: rules
name: Stormglass API Rules
provider_name: Stormglass
provider_slug: stormglass
rule_count: 9
rules:
- description: All point endpoints must require lat and lng query parameters
  given: $.paths[?(@property.match(/\/point$/))].get.parameters[?(@.in == 'query')]
  name: stormglass-coordinate-params-required
  severity: error
- description: All operations must use API key authentication via Authorization header
  given: $.paths.*.*
  name: stormglass-api-key-auth
  severity: warn
- description: All 200 responses should include a meta object with quota information
  given: $.paths.*.get.responses.200.content.application/json.schema
  name: stormglass-response-meta-object
  severity: warn
- description: All query parameters must have descriptions
  given: $.paths.*.*.parameters[?(@.in == 'query')]
  name: stormglass-params-description
  severity: warn
- description: All API paths should be versioned under /v2 (enforced at server level)
  given: $.servers[*]
  name: stormglass-v2-paths
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*]
  name: stormglass-https-only
  severity: error
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: stormglass-tags-defined
  severity: warn
- description: All operations must have an operationId
  given: $.paths.*.*
  name: stormglass-operation-ids
  severity: error
- description: All operations must have a summary
  given: $.paths.*.*
  name: stormglass-operation-summary
  severity: warn
rules_file: rules/stormglass-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stormglass/refs/heads/main/rules/stormglass-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: stormglass-rules
source_filename: stormglass-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stormglass-coordinate-params-required:\n    description: All point endpoints must require lat and lng query parameters\n    message: \"Point endpoint '{{path}}' must have required 'lat' and 'lng' query parameters\"\n    severity: error\n    given: \"$.paths[?(@property.match(/\\\\/point$/))].get.parameters[?(@.in == 'query')]\"\n    then:\n      field: required\n      function: truthy\n\n  stormglass-api-key-auth:\n    description: All operations must use API key authentication via Authorization header\n    message: \"Operations must declare apiKeyAuth security scheme\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: security\n      function: defined\n\n  stormglass-response-meta-object:\n    description: All 200 responses should include a meta object with quota information\n    message: \"Response schema should include a 'meta' property with quota information\"\n    severity: warn\n    given: \"$.paths.*.get.responses.200.content.application/json.schema\"\
  \n    then:\n      field: properties.meta\n      function: defined\n\n  stormglass-params-description:\n    description: All query parameters must have descriptions\n    message: \"Query parameter '{{property}}' must have a description\"\n    severity: warn\n    given: \"$.paths.*.*.parameters[?(@.in == 'query')]\"\n    then:\n      field: description\n      function: truthy\n\n  stormglass-v2-paths:\n    description: All API paths should be versioned under /v2 (enforced at server level)\n    message: \"Server URL should reference /v2 base path\"\n    severity: info\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.stormglass\\\\.io/v2\"\n\n  stormglass-https-only:\n    description: All server URLs must use HTTPS\n    message: \"Server URL '{{value}}' must use HTTPS\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n\
  \        match: \"^https://\"\n\n  stormglass-tags-defined:\n    description: All operations must have at least one tag\n    message: \"Operation at '{{path}}' must include at least one tag\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  stormglass-operation-ids:\n    description: All operations must have an operationId\n    message: \"Operation at '{{path}}' must have an operationId\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: truthy\n\n  stormglass-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation at '{{path}}' must have a summary\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: summary\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stormglass/refs/heads/main/rules/stormglass-rules.yml
tags:
- Astronomy
- Bio
- Climate
- Elevation
- Forecasting
- Marine
- Ocean
- Solar
- Tides
- Weather
- Wind
- Spectral
- Linting
- API Governance
---
