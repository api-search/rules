---
api_specs:
- filename: vitess-vtadmin-openapi.yml
  format: yaml
  label: Vitess VTAdmin API
  slug: vtadmin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vitess/refs/heads/main/openapi/vitess-vtadmin-openapi.yml
categories:
- vitess
description: Spectral linting rules defining API design standards and conventions for Vitess.
layout: rules
name: Vitess API Rules
provider_name: Vitess
provider_slug: vitess
rule_count: 9
rules:
- description: ''
  given: $.paths[*][*]
  name: vitess-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*].summary
  name: vitess-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][*].operationId
  name: vitess-operationid-camelcase
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: vitess-operation-tags
  severity: warn
- description: ''
  given: $.paths[*].get.responses
  name: vitess-get-200-response
  severity: error
- description: ''
  given: $.paths[*].get.responses
  name: vitess-get-500-response
  severity: hint
- description: ''
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: vitess-path-params-described
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: vitess-schema-descriptions
  severity: hint
- description: ''
  given: $.paths[*][*].parameters[?(@.in=='query')].name
  name: vitess-query-param-snake-case
  severity: warn
rules_file: rules/vitess-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vitess/refs/heads/main/rules/vitess-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 5
slug: vitess-rules
source_filename: vitess-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # All operations must have summaries\n  vitess-operation-summary-required:\n    message: \"All VTAdmin API operations must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case\n  vitess-summary-title-case:\n    message: \"Operation summaries must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operation IDs must use camelCase\n  vitess-operationid-camelcase:\n    message: \"Operation IDs must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Operations must be tagged\n  vitess-operation-tags:\n    message: \"All operations must have at least one tag\"\n    severity: warn\n   \
  \ given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  # GET operations return 200\n  vitess-get-200-response:\n    message: \"GET operations must document a 200 response\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # All GET operations must document 500 response\n  vitess-get-500-response:\n    message: \"GET operations should document a 500 error response\"\n    severity: hint\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"500\"\n      function: truthy\n\n  # Path parameters must have descriptions\n  vitess-path-params-described:\n    message: \"Path parameters must have descriptions\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n\n  # Schemas must have descriptions\n  vitess-schema-descriptions:\n    message: \"Component schemas must have descriptions\"\n   \
  \ severity: hint\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # API must use snake_case for query parameters (Vitess convention)\n  vitess-query-param-snake-case:\n    message: \"Query parameters must use snake_case (Vitess API convention)\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vitess/refs/heads/main/rules/vitess-rules.yml
tags:
- Cloud Native
- CNCF
- Database
- Distributed Systems
- Graduated
- MySQL
- Sharding
- Spectral
- Linting
- API Governance
---
