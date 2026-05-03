---
api_specs:
- filename: vks-api-openapi.yml
  format: yaml
  label: VKS API
  slug: vks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vks-integrations/refs/heads/main/openapi/vks-api-openapi.yml
categories:
- vks
description: Spectral linting rules defining API design standards and conventions for VKS Integrations.
layout: rules
name: VKS Integrations API Rules
provider_name: VKS Integrations
provider_slug: vks-integrations
rule_count: 8
rules:
- description: Operation IDs must use camelCase to match VKS API conventions.
  given: $.paths[*][*].operationId
  name: vks-operation-ids-camel-case
  severity: warn
- description: All VKS API operations require API key authentication.
  given: $.paths[*][*]
  name: vks-require-api-key-security
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: vks-require-summaries
  severity: error
- description: All operations and schemas must have descriptions.
  given:
  - $.paths[*][*]
  - $.components.schemas[*]
  name: vks-require-descriptions
  severity: warn
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: vks-path-params-documented
  severity: warn
- description: All authenticated operations must define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete]
  name: vks-require-401-response
  severity: warn
- description: All date/time fields must use format date-time.
  given: $.components.schemas[*].properties[*][?(@.type == 'string' && @.description)]
  name: vks-use-iso8601-dates
  severity: warn
- description: Collection endpoints must use plural noun paths.
  given: $.paths
  name: vks-work-order-paths-plural
  severity: warn
rules_file: rules/vks-integrations-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vks-integrations/refs/heads/main/rules/vks-integrations-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: vks-integrations-rules
source_filename: vks-integrations-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  vks-operation-ids-camel-case:\n    description: Operation IDs must use camelCase to match VKS API conventions.\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vks-require-api-key-security:\n    description: All VKS API operations require API key authentication.\n    message: \"Operation {{path}} must define security\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  vks-require-summaries:\n    description: All operations must have a summary.\n    message: \"Operation {{path}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  vks-require-descriptions:\n    description: All operations and schemas must have descriptions.\n  \
  \  message: \"{{path}} must have a description\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  vks-path-params-documented:\n    description: All path parameters must have descriptions.\n    message: \"Path parameter {{path}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  vks-require-401-response:\n    description: All authenticated operations must define a 401 Unauthorized response.\n    message: \"Authenticated operation {{path}} must define a 401 response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  vks-use-iso8601-dates:\n    description: All date/time fields must use format date-time.\n    message: \"Date field {{path}} must use format: date-time\"\
  \n    severity: warn\n    given: \"$.components.schemas[*].properties[*][?(@.type == 'string' && @.description)]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              description:\n                pattern: \"(created|updated|started|completed|recorded)\"\n          then:\n            required: [\"format\"]\n\n  vks-work-order-paths-plural:\n    description: Collection endpoints must use plural noun paths.\n    message: \"Collection paths must use plural nouns\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vks-integrations/refs/heads/main/rules/vks-integrations-rules.yml
tags:
- ERP Integration
- Manufacturing
- MES
- Operations Management
- Quality Management
- Work Instructions
- Work Orders
- Spectral
- Linting
- API Governance
---
