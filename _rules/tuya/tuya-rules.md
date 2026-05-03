---
categories:
- tuya
description: Spectral linting rules defining API design standards and conventions for Tuya.
layout: rules
name: Tuya API Rules
provider_name: Tuya
provider_slug: tuya
rule_count: 12
rules:
- description: All API paths must begin with a version segment like /v1.0/
  given: $.paths[*]~
  name: tuya-versioned-paths
  severity: error
- description: Parameter names must use snake_case
  given: $.paths[*][*].parameters[*].name
  name: tuya-snake-case-parameters
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: tuya-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: tuya-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: tuya-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tuya-summary-title-case
  severity: warn
- description: All 200 responses should include a success field in their schema
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: tuya-response-success-field
  severity: hint
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: tuya-operation-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: tuya-operation-tags-required
  severity: warn
- description: API must define a tuyaApiKey or equivalent apiKey security scheme
  given: $.components.securitySchemes
  name: tuya-security-scheme-apikey
  severity: warn
- description: At least one server must be defined
  given: $
  name: tuya-servers-defined
  severity: error
- description: All tags in info must use Title Case
  given: $.tags[*].name
  name: tuya-tags-title-case
  severity: warn
rules_file: rules/tuya-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tuya/refs/heads/main/rules/tuya-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 7
slug: tuya-rules
source_filename: tuya-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Tuya uses /v{version}/ prefix on all paths\n  tuya-versioned-paths:\n    description: All API paths must begin with a version segment like /v1.0/\n    message: \"Path '{{path}}' must begin with /v1.0/ or /v{version}/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\\\\.[0-9]+/\"\n\n  # Tuya uses snake_case for path parameters and query parameters\n  tuya-snake-case-parameters:\n    description: Parameter names must use snake_case\n    message: \"Parameter '{{value}}' must use snake_case\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # All operations must have an operationId\n  tuya-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: operationId\n      function: defined\n\n  # All operationIds must be camelCase\n  tuya-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have a summary\n  tuya-operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Summaries must use Title Case\n  tuya-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must begin with a capital letter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Tuya API responses use a standard wrapper with result, success, and t fields\n  tuya-response-success-field:\n    description: All 200 responses should include a success field in their schema\n    severity: hint\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      field: success\n      function: defined\n\n  # Require description on all operations\n  tuya-operation-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: defined\n\n  # Require tags on all operations\n  tuya-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # Tuya uses apiKey authentication\
  \ via client_id header\n  tuya-security-scheme-apikey:\n    description: API must define a tuyaApiKey or equivalent apiKey security scheme\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  # Require servers\n  tuya-servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: defined\n\n  # Tags must use Title Case\n  tuya-tags-title-case:\n    description: All tags in info must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tuya/refs/heads/main/rules/tuya-rules.yml
tags:
- IoT
- Smart Home
- Devices
- Cloud Platform
- Automation
- Industrial IoT
- Device Management
- Spectral
- Linting
- API Governance
---
