---
api_specs:
- filename: tiktok-business-openapi.yml
  format: yaml
  label: TikTok API for Business
  slug: tiktok-business-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok/refs/heads/main/openapi/tiktok-business-openapi.yml
- filename: tiktok-shop-openapi.yml
  format: yaml
  label: TikTok Shop API
  slug: tiktok-shop-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok/refs/heads/main/openapi/tiktok-shop-openapi.yml
- filename: tiktok-data-portability-openapi.yml
  format: yaml
  label: TikTok Data Portability API
  slug: tiktok-data-portability-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok/refs/heads/main/openapi/tiktok-data-portability-openapi.yml
categories:
- tiktok
description: Spectral linting rules defining API design standards and conventions for TikTok.
layout: rules
name: TikTok API Rules
provider_name: TikTok
provider_slug: tiktok
rule_count: 6
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tiktok-operation-id-camel-case
  severity: warn
- description: All paths must include an API version prefix
  given: $.paths
  name: tiktok-versioned-paths
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: tiktok-operation-summary
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: tiktok-operation-tags
  severity: warn
- description: Business API responses should include a code field
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: tiktok-business-api-code-field
  severity: info
- description: Business API operations should document advertiser_id parameter
  given: $.paths[*][get].parameters[*]
  name: tiktok-advertiser-id-required
  severity: info
rules_file: rules/tiktok-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tiktok/refs/heads/main/rules/tiktok-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 2
slug: tiktok-rules
source_filename: tiktok-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tiktok-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tiktok-versioned-paths:\n    description: All paths must include an API version prefix\n    message: \"Path '{{value}}' must start with a version prefix\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/(v[0-9]+|open_api/v[0-9]+)\"\n\n  tiktok-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tiktok-operation-tags:\n    description: All operations must have\
  \ tags\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tiktok-business-api-code-field:\n    description: Business API responses should include a code field\n    message: \"Business API response schema should have a 'code' field\"\n    severity: info\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  tiktok-advertiser-id-required:\n    description: Business API operations should document advertiser_id parameter\n    message: \"Endpoint should document advertiser_id parameter\"\n    severity: info\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tiktok/refs/heads/main/rules/tiktok-rules.yml
tags:
- Advertising
- Commerce
- Content
- E-Commerce
- Social Media
- Video
- Spectral
- Linting
- API Governance
---
