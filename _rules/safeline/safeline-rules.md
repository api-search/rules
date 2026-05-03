---
api_specs:
- filename: safeline-management-openapi.yml
  format: yaml
  label: SafeLine Management API
  slug: safeline
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/safeline/refs/heads/main/openapi/safeline-management-openapi.yml
categories:
- safeline
description: Spectral linting rules defining API design standards and conventions for SafeLine.
layout: rules
name: SafeLine API Rules
provider_name: SafeLine
provider_slug: safeline
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: safeline-operation-summary-title-case
  severity: warn
- description: All endpoints must use X-SLCE-API-Token header authentication
  given: $.paths[*][*]
  name: safeline-api-token-auth
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: safeline-operation-ids-camel-case
  severity: warn
- description: All responses should use SafeLine envelope format with err, data, msg
  given: $.components.schemas[*]
  name: safeline-response-envelope-format
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: safeline-tags-defined
  severity: warn
- description: SafeLine management API endpoints start with /api/ prefix
  given: $.paths
  name: safeline-management-endpoints-versioned
  severity: info
- description: List endpoints should support page and page_size parameters
  given: $.paths[*][get].parameters
  name: safeline-paginated-endpoints
  severity: info
- description: Security scheme must use apiKey type
  given: $.components.securitySchemes[*]
  name: safeline-security-scheme-apikey
  severity: error
rules_file: rules/safeline-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/safeline/refs/heads/main/rules/safeline-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 3
slug: safeline-rules
source_filename: safeline-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  safeline-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*)( [A-Z][a-z0-9]*)*$\"\n\n  safeline-api-token-auth:\n    description: All endpoints must use X-SLCE-API-Token header authentication\n    message: \"Endpoint must declare APITokenAuth security\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: security\n      function: defined\n\n  safeline-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  safeline-response-envelope-format:\n\
  \    description: All responses should use SafeLine envelope format with err, data, msg\n    message: \"SafeLine API responses should use envelope with err, data, msg fields\"\n    given: \"$.components.schemas[*]\"\n    severity: info\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  safeline-tags-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  safeline-management-endpoints-versioned:\n    description: SafeLine management API endpoints start with /api/ prefix\n    message: \"SafeLine API paths must start with /api/\"\n    given: \"$.paths\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/api\\\\/\"\n\n  safeline-paginated-endpoints:\n    description: List endpoints should support page and page_size\
  \ parameters\n    message: \"List endpoints should define pagination parameters\"\n    given: \"$.paths[*][get].parameters\"\n    severity: info\n    then:\n      function: defined\n\n  safeline-security-scheme-apikey:\n    description: Security scheme must use apiKey type\n    message: \"Security scheme must be of type apiKey for SafeLine\"\n    given: \"$.components.securitySchemes[*]\"\n    severity: error\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - apiKey\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/safeline/refs/heads/main/rules/safeline-rules.yml
tags:
- Proxy
- WAF
- Security
- Open Source
- Reverse Proxy
- API Gateway
- Spectral
- Linting
- API Governance
---
