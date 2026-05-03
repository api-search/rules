---
api_specs:
- filename: smartcar-vehicles-openapi.yml
  format: yaml
  label: Smartcar Vehicles API
  slug: vehicles-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smartcar/refs/heads/main/openapi/smartcar-vehicles-openapi.yml
categories:
- smartcar
description: Spectral linting rules defining API design standards and conventions for Smartcar.
layout: rules
name: Smartcar API Rules
provider_name: Smartcar
provider_slug: smartcar
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: smartcar-operation-id-camel-case
  severity: warn
- description: Vehicle endpoints must use {id} as path parameter
  given: $.paths[*]~
  name: smartcar-vehicle-id-path-param
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smartcar-operation-summary-title-case
  severity: warn
- description: Vehicle data endpoints should document their required permission in the description
  given: $.paths['/vehicles/{id}/*'][get]
  name: smartcar-permission-documented
  severity: info
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: smartcar-response-200-get
  severity: error
- description: All operations should use Bearer authentication
  given: $
  name: smartcar-bearer-auth-required
  severity: warn
- description: POST command endpoints should return a CommandResult or equivalent schema
  given: $.paths[*].post.responses.200.content.application/json.schema
  name: smartcar-command-result-schema
  severity: info
- description: Vehicle data endpoints should document 409 for vehicle state conflicts
  given: $.paths['/vehicles/{id}/*'][get]
  name: smartcar-error-409-vehicle-state
  severity: info
rules_file: rules/smartcar-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smartcar/refs/heads/main/rules/smartcar-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 4
slug: smartcar-rules
source_filename: smartcar-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Smartcar API Naming Conventions\n  smartcar-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' should use camelCase (e.g., getBatteryLevel)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  smartcar-vehicle-id-path-param:\n    description: Vehicle endpoints must use {id} as path parameter\n    message: \"Vehicle endpoints should use {id} for the vehicle identifier\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/vehicles(\\\\/\\\\{id\\\\}|$)\"\n\n  smartcar-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n  \
  \    function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z]*(\\\\s[A-Z][A-Za-z]*)*$\"\n\n  smartcar-permission-documented:\n    description: Vehicle data endpoints should document their required permission in the description\n    message: \"Vehicle data endpoint should mention required permission in description\"\n    severity: info\n    given: \"$.paths['/vehicles/{id}/*'][get]\"\n    then:\n      field: description\n      function: truthy\n\n  smartcar-response-200-get:\n    description: All GET operations must define a 200 response\n    message: \"GET operations must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  smartcar-bearer-auth-required:\n    description: All operations should use Bearer authentication\n    message: \"Operations should use BearerAuth security scheme\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function:\
  \ truthy\n\n  smartcar-command-result-schema:\n    description: POST command endpoints should return a CommandResult or equivalent schema\n    message: \"Command POST operations should reference a result schema\"\n    severity: info\n    given: \"$.paths[*].post.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n\n  smartcar-error-409-vehicle-state:\n    description: Vehicle data endpoints should document 409 for vehicle state conflicts\n    message: \"Vehicle telemetry endpoints should define 409 response for vehicle state conflicts\"\n    severity: info\n    given: \"$.paths['/vehicles/{id}/*'][get]\"\n    then:\n      field: responses.409\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smartcar/refs/heads/main/rules/smartcar-rules.yml
tags:
- Automotive
- Connected Vehicles
- IoT
- Mobility
- Fleet Management
- EV Management
- Telematics
- Spectral
- Linting
- API Governance
---
