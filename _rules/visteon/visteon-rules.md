---
api_specs:
- filename: visteon-phoenix-openapi.yml
  format: yaml
  label: Visteon Phoenix API
  slug: phoenix-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/visteon/refs/heads/main/openapi/visteon-phoenix-openapi.yml
categories:
- visteon
description: Spectral linting rules defining API design standards and conventions for Visteon.
layout: rules
name: Visteon API Rules
provider_name: Visteon
provider_slug: visteon
rule_count: 10
rules:
- description: ''
  given: $.paths[*][*]
  name: visteon-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*].summary
  name: visteon-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][*].operationId
  name: visteon-operationid-camelcase
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: visteon-operation-tags
  severity: warn
- description: ''
  given: $.paths[*].get.responses
  name: visteon-get-200-response
  severity: error
- description: ''
  given: $.paths[*].post.responses
  name: visteon-post-201-response
  severity: warn
- description: ''
  given: $.paths[*].delete.responses
  name: visteon-delete-204-response
  severity: hint
- description: ''
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: visteon-path-params-described
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: visteon-schema-descriptions
  severity: hint
- description: ''
  given: $.paths[*].put
  name: visteon-put-has-body
  severity: error
rules_file: rules/visteon-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/visteon/refs/heads/main/rules/visteon-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 5
slug: visteon-rules
source_filename: visteon-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # All operations must have a summary\n  visteon-operation-summary-required:\n    message: \"All Visteon Phoenix API operations must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case\n  visteon-summary-title-case:\n    message: \"Operation summaries must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Operation IDs must use camelCase\n  visteon-operationid-camelcase:\n    message: \"Operation IDs must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must be tagged\n  visteon-operation-tags:\n    message: \"All operations must have at least one tag\"\
  \n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  # GET responses must return 200\n  visteon-get-200-response:\n    message: \"GET operations must return a 200 response\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # POST create operations return 201\n  visteon-post-201-response:\n    message: \"POST create operations should return 201\"\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  # DELETE operations return 204\n  visteon-delete-204-response:\n    message: \"DELETE operations should return 204\"\n    severity: hint\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  # Path parameters must be described\n  visteon-path-params-described:\n    message: \"All path parameters must have a description\"\n    severity: warn\n\
  \    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n\n  # Schemas must have descriptions\n  visteon-schema-descriptions:\n    message: \"All component schemas must have descriptions\"\n    severity: hint\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PUT operations must have request bodies\n  visteon-put-has-body:\n    message: \"PUT operations must include a requestBody\"\n    severity: error\n    given: \"$.paths[*].put\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/visteon/refs/heads/main/rules/visteon-rules.yml
tags:
- Automotive
- Connected Car
- Infotainment
- IoT
- Spectral
- Linting
- API Governance
---
