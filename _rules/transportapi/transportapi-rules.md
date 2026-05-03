---
api_specs:
- filename: transportapi-openapi.yml
  format: yaml
  label: TransportAPI
  slug: transportapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/transportapi/refs/heads/main/openapi/transportapi-openapi.yml
categories:
- transportapi
description: Spectral linting rules defining API design standards and conventions for TransportAPI.
layout: rules
name: TransportAPI API Rules
provider_name: TransportAPI
provider_slug: transportapi
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: transportapi-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: transportapi-operationid-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: transportapi-tags-required
  severity: warn
- description: UK transport endpoints should end with .json extension
  given: $.paths
  name: transportapi-json-extension-in-paths
  severity: hint
- description: All GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: transportapi-response-200-required
  severity: error
- description: API authentication via app_id and app_key query parameters must be documented
  given: $.components.securitySchemes
  name: transportapi-app-auth-params
  severity: warn
- description: All paths should operate under UK data context
  given: $.servers[*].url
  name: transportapi-uk-base-path
  severity: info
- description: Bus stop path parameters should be named atcocode
  given: $.paths[*][*].parameters[*][?(@.in=='path' && @.name=='station_stop')]
  name: transportapi-atcocode-path-param
  severity: hint
- description: Date-time properties should use ISO 8601 format
  given: $.components.schemas[*].properties[?(@.format=='date-time')]
  name: transportapi-datetime-format
  severity: warn
- description: Collection endpoints should support limit parameter
  given: $.paths[*].get.parameters[*][?(@.name=='limit')]
  name: transportapi-pagination-limit
  severity: hint
rules_file: rules/transportapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/transportapi/refs/heads/main/rules/transportapi-rules.yml
severity_counts:
  error: 2
  hint: 3
  info: 1
  warn: 4
slug: transportapi-rules
source_filename: transportapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  transportapi-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  transportapi-operationid-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  transportapi-tags-required:\n    description: All operations must have tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  transportapi-json-extension-in-paths:\n    description: UK transport endpoints should end with .json extension\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n\
  \            \".*\\\\.json$\": {}\n\n  transportapi-response-200-required:\n    description: All GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  transportapi-app-auth-params:\n    description: API authentication via app_id and app_key query parameters must be documented\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  transportapi-uk-base-path:\n    description: All paths should operate under UK data context\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*transportapi\\\\.com.*\"\n\n  transportapi-atcocode-path-param:\n    description: Bus stop path parameters should be named atcocode\n    severity: hint\n    given: \"$.paths[*][*].parameters[*][?(@.in=='path' && @.name=='station_stop')]\"\n    then:\n      function: falsy\n\n  transportapi-datetime-format:\n\
  \    description: Date-time properties should use ISO 8601 format\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.format=='date-time')]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  transportapi-pagination-limit:\n    description: Collection endpoints should support limit parameter\n    severity: hint\n    given: \"$.paths[*].get.parameters[*][?(@.name=='limit')]\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/transportapi/refs/heads/main/rules/transportapi-rules.yml
tags:
- Public Transit
- Transport
- UK
- Real-Time
- Journey Planning
- Bus
- Rail
- Spectral
- Linting
- API Governance
---
