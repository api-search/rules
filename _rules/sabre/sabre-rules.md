---
api_specs:
- filename: sabre-bargain-finder-max-openapi.yml
  format: yaml
  label: Sabre Bargain Finder Max API
  slug: bargain-finder-max
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sabre/refs/heads/main/openapi/sabre-bargain-finder-max-openapi.yml
- filename: sabre-hotels-openapi.yml
  format: yaml
  label: Sabre Hotels API
  slug: hotels
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sabre/refs/heads/main/openapi/sabre-hotels-openapi.yml
categories:
- sabre
description: Spectral linting rules defining API design standards and conventions for Sabre.
layout: rules
name: Sabre API Rules
provider_name: Sabre
provider_slug: sabre
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sabre-operation-summary-title-case
  severity: warn
- description: All endpoints except authentication must require BearerAuth
  given: $.paths[*][*]
  name: sabre-bearer-auth-required
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: sabre-operation-ids-camel-case
  severity: warn
- description: OTA request/response schemas should use OTA naming convention
  given: $.components.schemas
  name: sabre-ota-schema-names
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: sabre-tags-required
  severity: warn
- description: Sabre API paths should include version prefix
  given: $.paths
  name: sabre-versioned-paths
  severity: info
- description: Operations should define 429 rate limit response
  given: $.paths[*][get,post].responses
  name: sabre-rate-limit-response
  severity: info
- description: Error responses should use standard Sabre error format
  given: $.paths[*][*].responses[4*,5*].content[*].schema
  name: sabre-error-response-structure
  severity: info
- description: POST operations must define a request body
  given: $.paths[*][post]
  name: sabre-post-request-body-required
  severity: error
rules_file: rules/sabre-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sabre/refs/heads/main/rules/sabre-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 4
  warn: 4
slug: sabre-rules
source_filename: sabre-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sabre-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*)( [A-Z][a-z0-9]*)*$\"\n\n  sabre-bearer-auth-required:\n    description: All endpoints except authentication must require BearerAuth\n    message: \"Endpoint must declare BearerAuth security\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: security\n      function: defined\n\n  sabre-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sabre-ota-schema-names:\n\
  \    description: OTA request/response schemas should use OTA naming convention\n    message: \"Sabre OTA schemas should follow OTA_* naming pattern\"\n    given: \"$.components.schemas\"\n    severity: info\n    then:\n      function: defined\n\n  sabre-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  sabre-versioned-paths:\n    description: Sabre API paths should include version prefix\n    message: \"Sabre API paths should include version (e.g., /v4.0.0/)\"\n    given: \"$.paths\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v[0-9]\"\n\n  sabre-rate-limit-response:\n    description: Operations should define 429 rate limit response\n    message: \"Operations should define 429 rate limit exceeded response\"\n    given: \"$.paths[*][get,post].responses\"\
  \n    severity: info\n    then:\n      field: \"429\"\n      function: defined\n\n  sabre-error-response-structure:\n    description: Error responses should use standard Sabre error format\n    message: \"Error responses should use standard Sabre ErrorResponse schema\"\n    given: \"$.paths[*][*].responses[4*,5*].content[*].schema\"\n    severity: info\n    then:\n      function: defined\n\n  sabre-post-request-body-required:\n    description: POST operations must define a request body\n    message: \"POST operations must include a requestBody\"\n    given: \"$.paths[*][post]\"\n    severity: error\n    then:\n      field: requestBody\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sabre/refs/heads/main/rules/sabre-rules.yml
tags:
- Travel
- GDS
- Airlines
- Hotels
- Car Rental
- Booking
- Spectral
- Linting
- API Governance
---
