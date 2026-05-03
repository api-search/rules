---
api_specs:
- filename: telefono-validation-openapi.yml
  format: yaml
  label: Telefono Phone Validation API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefono/refs/heads/main/openapi/telefono-validation-openapi.yml
- filename: telefono-carrier-openapi.yml
  format: yaml
  label: Telefono Carrier Lookup API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefono/refs/heads/main/openapi/telefono-carrier-openapi.yml
- filename: telefono-format-openapi.yml
  format: yaml
  label: Telefono Number Formatting API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefono/refs/heads/main/openapi/telefono-format-openapi.yml
categories:
- telefono
description: Spectral linting rules defining API design standards and conventions for Telefono.
layout: rules
name: Telefono API Rules
provider_name: Telefono
provider_slug: telefono
rule_count: 11
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telefono-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telefono-operation-must-have-operationid
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: telefono-operationid-camelcase
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: telefono-operation-must-have-description
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: telefono-operation-must-have-tag
  severity: warn
- description: Validation and lookup endpoints must require the 'number' parameter
  given: $.paths['/validate'].get.parameters[?(@.name == 'number')]
  name: telefono-number-parameter-required
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: telefono-response-200-required
  severity: error
- description: All operations should define a 400 Bad Request response
  given: $.paths[*][*].responses
  name: telefono-400-error-response
  severity: warn
- description: All schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: telefono-schema-properties-have-description
  severity: info
- description: API must define ApiKeyAuth security scheme
  given: $.components.securitySchemes
  name: telefono-api-key-security
  severity: error
- description: API must define servers
  given: $
  name: telefono-servers-required
  severity: error
rules_file: rules/telefono-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telefono/refs/heads/main/rules/telefono-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 4
slug: telefono-rules
source_filename: telefono-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  telefono-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  telefono-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  telefono-operationid-camelcase:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telefono-operation-must-have-description:\n    description: All operations should have a description\n    severity: info\n    given:\
  \ \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefono-operation-must-have-tag:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telefono-number-parameter-required:\n    description: Validation and lookup endpoints must require the 'number' parameter\n    severity: error\n    given: \"$.paths['/validate'].get.parameters[?(@.name == 'number')]\"\n    then:\n      field: required\n      function: truthy\n\n  telefono-response-200-required:\n    description: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  telefono-400-error-response:\n    description: All operations should define a 400 Bad Request response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"400\"\n      function: truthy\n\
  \n  telefono-schema-properties-have-description:\n    description: All schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefono-api-key-security:\n    description: API must define ApiKeyAuth security scheme\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: ApiKeyAuth\n      function: truthy\n\n  telefono-servers-required:\n    description: API must define servers\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telefono/refs/heads/main/rules/telefono-rules.yml
tags:
- Carrier Lookup
- Data Enrichment
- Fraud Prevention
- Number Intelligence
- Number Verification
- Phone Lookup
- Phone Validation
- Telecommunications
- Spectral
- Linting
- API Governance
---
