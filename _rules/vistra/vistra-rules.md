---
api_specs:
- filename: vistra-incorporations-openapi.yml
  format: yaml
  label: Vistra Incorporations API
  slug: incorporations-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vistra/refs/heads/main/openapi/vistra-incorporations-openapi.yml
categories:
- vistra
description: Spectral linting rules defining API design standards and conventions for Vistra.
layout: rules
name: Vistra API Rules
provider_name: Vistra
provider_slug: vistra
rule_count: 11
rules:
- description: ''
  given: $.paths[*][*]
  name: vistra-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*].summary
  name: vistra-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][*].operationId
  name: vistra-operationid-camelcase
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: vistra-operation-tags
  severity: warn
- description: ''
  given: $.paths[*].post.responses
  name: vistra-post-201
  severity: warn
- description: ''
  given: $.paths[*].get.responses
  name: vistra-get-200
  severity: error
- description: ''
  given: $.paths[*][*].responses
  name: vistra-401-documented
  severity: warn
- description: ''
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: vistra-path-params-described
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: vistra-schema-descriptions
  severity: hint
- description: ''
  given: $.paths[*].post
  name: vistra-post-has-body
  severity: error
- description: ''
  given: $.paths[*][*]
  name: vistra-oauth2-security
  severity: warn
rules_file: rules/vistra-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vistra/refs/heads/main/rules/vistra-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 7
slug: vistra-rules
source_filename: vistra-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Operations must have summaries\n  vistra-operation-summary-required:\n    message: \"All Vistra API operations must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case\n  vistra-summary-title-case:\n    message: \"Operation summaries must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Operation IDs must be camelCase\n  vistra-operationid-camelcase:\n    message: \"Operation IDs must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must be tagged\n  vistra-operation-tags:\n    message: \"All operations must have at least one tag\"\n    severity:\
  \ warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  # POST create operations return 201\n  vistra-post-201:\n    message: \"POST operations creating resources should return 201\"\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  # GET returns 200\n  vistra-get-200:\n    message: \"GET operations must return 200 for success\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # All endpoints must document 401 response\n  vistra-401-documented:\n    message: \"All endpoints should document 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Path parameters must be described\n  vistra-path-params-described:\n    message: \"Path parameters must have descriptions\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  # All schemas should have descriptions\n  vistra-schema-descriptions:\n    message: \"Component schemas should have descriptions\"\n    severity: hint\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # POST operations must have request bodies\n  vistra-post-has-body:\n    message: \"POST operations must include a requestBody\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # API must use OAuth2\n  vistra-oauth2-security:\n    message: \"All Vistra API paths should use OAuth2Bearer security\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vistra/refs/heads/main/rules/vistra-rules.yml
tags:
- Compliance
- Corporate Services
- Entity Management
- Finance
- Fortune 500
- Legal
- Spectral
- Linting
- API Governance
---
