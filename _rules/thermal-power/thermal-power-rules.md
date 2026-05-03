---
api_specs:
- filename: thermal-power-openapi.yml
  format: yaml
  label: Thermal Power API
  slug: thermal-power
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thermal-power/refs/heads/main/openapi/thermal-power-openapi.yml
categories:
- thermal
description: Spectral linting rules defining API design standards and conventions for Thermal Power.
layout: rules
name: Thermal Power API Rules
provider_name: Thermal Power
provider_slug: thermal-power
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thermal-power-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: thermal-power-operation-ids-camel-case
  severity: warn
- description: All operations must require api_key query parameter.
  given: $.paths[*][get,post].parameters[?(@.name == 'api_key')]
  name: thermal-power-api-key-required
  severity: error
- description: All list operations should support offset and length pagination.
  given: $.paths[*][get]
  name: thermal-power-pagination-params
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: thermal-power-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: thermal-power-description-required
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths[*][get].responses
  name: thermal-power-200-response-defined
  severity: error
- description: EIA API data paths should end with /data.
  given: $.paths[*]~
  name: thermal-power-path-data-suffix
  severity: info
rules_file: rules/thermal-power-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thermal-power/refs/heads/main/rules/thermal-power-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: thermal-power-rules
source_filename: thermal-power-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  thermal-power-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  thermal-power-operation-ids-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  thermal-power-api-key-required:\n    description: All operations must require api_key query parameter.\n    message: \"Operation at '{{path}}' must define api_key as a required query parameter.\"\n    severity: error\n    given: \"$.paths[*][get,post].parameters[?(@.name == 'api_key')]\"\n    then:\n      field: required\n\
  \      function: truthy\n\n  thermal-power-pagination-params:\n    description: All list operations should support offset and length pagination.\n    message: \"List operation at '{{path}}' should support offset/length pagination.\"\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  thermal-power-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  thermal-power-description-required:\n    description: All operations must have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  thermal-power-200-response-defined:\n\
  \    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  thermal-power-path-data-suffix:\n    description: EIA API data paths should end with /data.\n    message: \"Path '{{path}}' should follow EIA pattern ending with /data.\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\/data$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thermal-power/refs/heads/main/rules/thermal-power-rules.yml
tags:
- Energy
- Thermal Power
- Power Generation
- Electricity
- Coal
- Natural Gas
- Nuclear
- Spectral
- Linting
- API Governance
---
