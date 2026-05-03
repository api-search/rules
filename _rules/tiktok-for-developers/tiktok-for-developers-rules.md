---
api_specs:
- filename: tiktok-display-openapi.yml
  format: yaml
  label: TikTok Display API
  slug: tiktok-display-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/openapi/tiktok-display-openapi.yml
- filename: tiktok-content-posting-openapi.yml
  format: yaml
  label: TikTok Content Posting API
  slug: tiktok-content-posting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/openapi/tiktok-content-posting-openapi.yml
- filename: tiktok-research-openapi.yml
  format: yaml
  label: TikTok Research API
  slug: tiktok-research-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/openapi/tiktok-research-openapi.yml
- filename: tiktok-login-kit-openapi.yml
  format: yaml
  label: TikTok Login Kit
  slug: tiktok-login-kit
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/openapi/tiktok-login-kit-openapi.yml
categories:
- tiktok
description: Spectral linting rules defining API design standards and conventions for TikTok for Developers.
layout: rules
name: TikTok for Developers API Rules
provider_name: TikTok for Developers
provider_slug: tiktok-for-developers
rule_count: 9
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tiktok-operation-id-camel-case
  severity: warn
- description: TikTok API paths must end with a trailing slash
  given: $.paths
  name: tiktok-path-trailing-slash
  severity: warn
- description: All paths must include an API version prefix
  given: $.paths
  name: tiktok-versioned-paths
  severity: error
- description: All operations must use Bearer authentication
  given: $.paths[*][*]
  name: tiktok-bearer-auth
  severity: error
- description: Successful responses should wrap data in a data envelope
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: tiktok-response-data-wrapper
  severity: warn
- description: Successful responses should include an error object for consistent error signaling
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: tiktok-error-object
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: tiktok-operation-summary-present
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: tiktok-operation-tags
  severity: warn
- description: GET and POST endpoints that return data should support a fields query parameter
  given: $.paths[*][get,post].parameters[*]
  name: tiktok-fields-query-param
  severity: info
rules_file: rules/tiktok-for-developers-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/rules/tiktok-for-developers-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: tiktok-for-developers-rules
source_filename: tiktok-for-developers-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tiktok-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tiktok-path-trailing-slash:\n    description: TikTok API paths must end with a trailing slash\n    message: \"Path '{{path}}' must end with a trailing slash per TikTok API convention\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \".*/$\"\n\n  tiktok-versioned-paths:\n    description: All paths must include an API version prefix\n    message: \"Path '{{value}}' must start with /v2/ version prefix\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^/v[0-9]+/\"\n\n  tiktok-bearer-auth:\n    description: All operations must use Bearer authentication\n    message: \"Operation must use BearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  tiktok-response-data-wrapper:\n    description: Successful responses should wrap data in a data envelope\n    message: \"Response 200 schema should have a 'data' property\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - data\n\n  tiktok-error-object:\n    description: Successful responses should include an error object for consistent error signaling\n    message:\
  \ \"Response 200 schema should include an 'error' property\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - error\n\n  tiktok-operation-summary-present:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tiktok-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tiktok-fields-query-param:\n    description: GET and POST endpoints that return data should support a fields query parameter\n    message: \"Endpoint should support a 'fields' query parameter\
  \ for field selection\"\n    severity: info\n    given: \"$.paths[*][get,post].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            name:\n              type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tiktok-for-developers/refs/heads/main/rules/tiktok-for-developers-rules.yml
tags:
- Advertising
- Analytics
- Authentication
- Content
- Social Media
- Video
- Spectral
- Linting
- API Governance
---
