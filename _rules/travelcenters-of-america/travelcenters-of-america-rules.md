---
api_specs:
- filename: travelcenters-of-america-openapi.yml
  format: yaml
  label: TravelCenters of America API
  slug: travelcenters-of-america
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/travelcenters-of-america/refs/heads/main/openapi/travelcenters-of-america-openapi.yml
categories:
- ta
description: Spectral linting rules defining API design standards and conventions for TravelCenters of America.
layout: rules
name: TravelCenters of America API Rules
provider_name: TravelCenters of America
provider_slug: travelcenters-of-america
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ta-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: ta-operationid-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: ta-tags-required
  severity: warn
- description: API must use API key authentication
  given: $.components.securitySchemes[*]
  name: ta-api-key-auth
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: ta-response-200-required
  severity: error
- description: Location-based queries should use location_id parameter consistently
  given: $.paths[*][*].parameters[*][?(@.name=='location_id')]
  name: ta-location-id-param
  severity: hint
- description: URL paths should use kebab-case for multi-word segments
  given: $.paths
  name: ta-kebab-case-paths
  severity: warn
- description: Responses should wrap data in a data property
  given: $.components.schemas[?(@property.match(/Response$/))].properties
  name: ta-data-wrapper
  severity: warn
- description: Availability responses should include a timestamp field
  given: $.components.schemas[?(@property.match(/Availability$/))].properties
  name: ta-timestamp-responses
  severity: hint
- description: List responses should include a total count
  given: $.components.schemas[?(@property.match(/ListResponse$/))].properties
  name: ta-pagination-for-lists
  severity: hint
rules_file: rules/travelcenters-of-america-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/travelcenters-of-america/refs/heads/main/rules/travelcenters-of-america-rules.yml
severity_counts:
  error: 3
  hint: 3
  info: 0
  warn: 4
slug: travelcenters-of-america-rules
source_filename: travelcenters-of-america-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ta-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  ta-operationid-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  ta-tags-required:\n    description: All operations must have tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  ta-api-key-auth:\n    description: API must use API key authentication\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - apiKey\n          - http\n\n  ta-response-200-required:\n\
  \    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  ta-location-id-param:\n    description: Location-based queries should use location_id parameter consistently\n    severity: hint\n    given: \"$.paths[*][*].parameters[*][?(@.name=='location_id')]\"\n    then:\n      field: schema\n      function: truthy\n\n  ta-kebab-case-paths:\n    description: URL paths should use kebab-case for multi-word segments\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^/[a-z][a-z0-9-/{}]*$\": {}\n\n  ta-data-wrapper:\n    description: Responses should wrap data in a data property\n    severity: warn\n    given: \"$.components.schemas[?(@property.match(/Response$/))].properties\"\n    then:\n      field: data\n      function: truthy\n\n \
  \ ta-timestamp-responses:\n    description: Availability responses should include a timestamp field\n    severity: hint\n    given: \"$.components.schemas[?(@property.match(/Availability$/))].properties\"\n    then:\n      field: timestamp\n      function: truthy\n\n  ta-pagination-for-lists:\n    description: List responses should include a total count\n    severity: hint\n    given: \"$.components.schemas[?(@property.match(/ListResponse$/))].properties\"\n    then:\n      field: total\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/travelcenters-of-america/refs/heads/main/rules/travelcenters-of-america-rules.yml
tags:
- Travel Centers
- Truck Service
- Retail
- Fuel
- Locations
- Trucking
- Fleet Management
- Spectral
- Linting
- API Governance
---
