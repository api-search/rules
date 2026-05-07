---
api_specs:
- filename: mobileapi-openapi.yml
  format: yaml
  label: MobileAPI
  slug: mobileapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/mobileapi-dev/refs/heads/main/openapi/mobileapi-openapi.yml
categories:
- mobileapi
description: Spectral linting rules defining API design standards and conventions for MobileAPI.dev.
layout: rules
name: MobileAPI.dev API Rules
provider_name: MobileAPI.dev
provider_slug: mobileapi-dev
rule_count: 11
rules:
- description: Every operation must have a summary.
  given: $.paths.*[get,post,put,patch,delete]
  name: mobileapi-operation-summary-required
  severity: error
- description: Operation summaries should be in Title Case (first word capitalized, no trailing period).
  given: $.paths.*[get,post,put,patch,delete].summary
  name: mobileapi-operation-summary-title-case
  severity: warn
- description: Tags should be lowercase, hyphen-separated.
  given: $.paths.*[get,post,put,patch,delete].tags[*]
  name: mobileapi-tags-lowercase-hyphen
  severity: warn
- description: Every operation must declare an operationId.
  given: $.paths.*[get,post,put,patch,delete]
  name: mobileapi-operation-id-required
  severity: error
- description: Paths should end with a trailing slash (Django convention).
  given: $.paths
  name: mobileapi-path-trailing-slash
  severity: warn
- description: Every operation should declare a 2xx success response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: mobileapi-success-response-required
  severity: warn
- description: Authenticated operations should document a 401 response.
  given: $.paths[?(@property != '/api-token-auth/' && @property != '/status/' && @property != '/payment_successful' && @property != '/payment_successful/')]*[get,post,put,patch,delete].responses
  name: mobileapi-unauthorized-response-documented
  severity: info
- description: Operations that consume credits should document a 429 Too Many Requests response.
  given: $.paths[?(@property != '/api-token-auth/' && @property != '/status/')]*[get,post,put,patch,delete].responses
  name: mobileapi-rate-limit-response-documented
  severity: info
- description: Resource schemas should include an 'id' property as primary key.
  given: $.components.schemas[?(@.type == 'object')]
  name: mobileapi-schema-id-property
  severity: info
- description: Document Authorization header as primary auth, query parameter as fallback only.
  given: $.components.securitySchemes
  name: mobileapi-prefer-header-auth
  severity: info
- description: Production server URL must use HTTPS.
  given: $.servers[*].url
  name: mobileapi-https-server
  severity: error
rules_file: rules/mobileapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/mobileapi-dev/refs/heads/main/rules/mobileapi-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 4
  warn: 4
slug: mobileapi-rules
source_filename: mobileapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  # MobileAPI.dev: every operation must declare a summary in Title Case.\n  mobileapi-operation-summary-required:\n    description: Every operation must have a summary.\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: summary\n      function: truthy\n\n  mobileapi-operation-summary-title-case:\n    description: Operation summaries should be in Title Case (first word capitalized, no trailing period).\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z\\\\[].*[^\\\\.]$\"\n\n  # MobileAPI.dev: tags must use lowercase-hyphenated form (Django REST Framework default).\n  mobileapi-tags-lowercase-hyphen:\n    description: Tags should be lowercase, hyphen-separated.\n    given: \"$.paths.*[get,post,put,patch,delete].tags[*]\"\n    severity: warn\n    then:\n      function: pattern\n   \
  \   functionOptions:\n        match: \"^[a-z0-9][a-z0-9\\\\-]*$\"\n\n  # MobileAPI.dev: every operation must declare an operationId for client codegen.\n  mobileapi-operation-id-required:\n    description: Every operation must declare an operationId.\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  # MobileAPI.dev: paths use a trailing slash (Django REST Framework convention).\n  mobileapi-path-trailing-slash:\n    description: Paths should end with a trailing slash (Django convention).\n    given: \"$.paths\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/$\"\n      field: \"@key\"\n\n  # MobileAPI.dev: every operation should declare a 200/201 response.\n  mobileapi-success-response-required:\n    description: Every operation should declare a 2xx success response.\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    severity: warn\n\
  \    then:\n      function: truthy\n      field: \"200\"\n\n  # MobileAPI.dev: every operation should document a 401 Unauthorized response.\n  mobileapi-unauthorized-response-documented:\n    description: Authenticated operations should document a 401 response.\n    given: \"$.paths[?(@property != '/api-token-auth/' && @property != '/status/' && @property != '/payment_successful' && @property != '/payment_successful/')]*[get,post,put,patch,delete].responses\"\n    severity: info\n    then:\n      function: truthy\n      field: \"401\"\n\n  # MobileAPI.dev: rate-limited operations should document 429 responses.\n  mobileapi-rate-limit-response-documented:\n    description: Operations that consume credits should document a 429 Too Many Requests response.\n    given: \"$.paths[?(@property != '/api-token-auth/' && @property != '/status/')]*[get,post,put,patch,delete].responses\"\n    severity: info\n    then:\n      function: truthy\n      field: \"429\"\n\n  # MobileAPI.dev: schemas should\
  \ include id and human-readable name where applicable.\n  mobileapi-schema-id-property:\n    description: Resource schemas should include an 'id' property as primary key.\n    given: \"$.components.schemas[?(@.type == 'object')]\"\n    severity: info\n    then:\n      field: properties.id\n      function: truthy\n\n  # MobileAPI.dev: prefer ApiKeyHeader (Authorization) over ApiKeyQuery for production traffic.\n  mobileapi-prefer-header-auth:\n    description: Document Authorization header as primary auth, query parameter as fallback only.\n    given: \"$.components.securitySchemes\"\n    severity: info\n    then:\n      field: ApiKeyHeader\n      function: truthy\n\n  # MobileAPI.dev: server URL should be HTTPS only in production.\n  mobileapi-https-server:\n    description: Production server URL must use HTTPS.\n    given: \"$.servers[*].url\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/mobileapi-dev/refs/heads/main/rules/mobileapi-rules.yml
tags:
- Data API
- Developer Tools
- Device Specifications
- Mobile Data
- Phone Specs
- REST API
- SaaS
- Spectral
- Linting
- API Governance
---
