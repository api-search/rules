---
api_specs:
- filename: rainbow-ai-nowcast-openapi.yml
  format: yaml
  label: Rainbow.AI Nowcast API
  slug: rainbow-ai-nowcast
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rainbow-ai/refs/heads/main/openapi/rainbow-ai-nowcast-openapi.yml
- filename: rainbow-ai-tiles-openapi.yml
  format: yaml
  label: Rainbow.AI Tiles API
  slug: rainbow-ai-tiles
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rainbow-ai/refs/heads/main/openapi/rainbow-ai-tiles-openapi.yml
categories:
- rainbow
description: Spectral linting rules defining API design standards and conventions for Rainbow.AI.
layout: rules
name: Rainbow.AI API Rules
provider_name: Rainbow.AI
provider_slug: rainbow-ai
rule_count: 8
rules:
- description: Rainbow.AI APIs must use Ocp-Apim-Subscription-Key header or token query parameter for authentication
  given: $.components.securitySchemes[*]
  name: rainbow-ai-api-key-auth
  severity: error
- description: Geolocation endpoints must include lat and lon query parameters
  given: $.paths[*].get.parameters[*]
  name: rainbow-ai-coordinate-params
  severity: warn
- description: Map tile paths must follow XYZ tiling scheme {z}/{x}/{y}
  given: $.paths
  name: rainbow-ai-tile-path-format
  severity: warn
- description: Weather data responses should include an updated_at timestamp
  given: $.components.schemas[*].properties
  name: rainbow-ai-response-updated-at
  severity: warn
- description: All operations must have appropriate weather-domain tags
  given: $.paths[*][*].tags
  name: rainbow-ai-weather-tags
  severity: warn
- description: All operations must have unique operationId in camelCase
  given: $.paths[*][*]
  name: rainbow-ai-operation-ids
  severity: error
- description: All endpoints must document a 429 Too Many Requests response
  given: $.paths[*].get.responses
  name: rainbow-ai-rate-limit-response
  severity: warn
- description: Rainbow.AI weather endpoints return bounded data sets and do not require pagination
  given: $.paths[*]
  name: rainbow-ai-pagination-not-required
  severity: hint
rules_file: rules/rainbow-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rainbow-ai/refs/heads/main/rules/rainbow-ai-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 5
slug: rainbow-ai-rules
source_filename: rainbow-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rainbow-ai-api-key-auth:\n    description: Rainbow.AI APIs must use Ocp-Apim-Subscription-Key header or token query parameter for authentication\n    message: Security scheme must use apiKey type with Ocp-Apim-Subscription-Key header or token query param\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              enum: [apiKey]\n          required: [type]\n\n  rainbow-ai-coordinate-params:\n    description: Geolocation endpoints must include lat and lon query parameters\n    message: Endpoint accepting coordinates must have lat and lon query parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters[*]\"\n    then:\n      function: truthy\n\n  rainbow-ai-tile-path-format:\n    description: Map tile paths must follow XYZ tiling scheme {z}/{x}/{y}\n    message: Tile paths\
  \ must use {z}/{x}/{y} path parameter pattern\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: truthy\n\n  rainbow-ai-response-updated-at:\n    description: Weather data responses should include an updated_at timestamp\n    message: Weather response schemas should have an updated_at field\n    severity: warn\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: truthy\n\n  rainbow-ai-weather-tags:\n    description: All operations must have appropriate weather-domain tags\n    message: Operation must be tagged with at least one weather-domain tag\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: truthy\n\n  rainbow-ai-operation-ids:\n    description: All operations must have unique operationId in camelCase\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  rainbow-ai-rate-limit-response:\n    description:\
  \ All endpoints must document a 429 Too Many Requests response\n    message: API endpoint must include 429 response code\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  rainbow-ai-pagination-not-required:\n    description: Rainbow.AI weather endpoints return bounded data sets and do not require pagination\n    message: Note - no pagination required for weather endpoints\n    severity: hint\n    given: \"$.paths[*]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rainbow-ai/refs/heads/main/rules/rainbow-ai-rules.yml
tags:
- Weather
- Precipitation
- Forecasting
- Nowcast
- Radar
- Tiles
- Geospatial
- Spectral
- Linting
- API Governance
---
