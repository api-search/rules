---
api_specs:
- filename: siemens-building-operations-openapi.yml
  format: yaml
  label: Siemens Building Operations API
  slug: building-operations-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/siemens/refs/heads/main/openapi/siemens-building-operations-openapi.yml
categories:
- siemens
description: Spectral linting rules defining API design standards and conventions for Siemens.
layout: rules
name: Siemens API Rules
provider_name: Siemens
provider_slug: siemens
rule_count: 8
rules:
- description: Siemens Building X APIs must use Bearer token authentication
  given: $.components.securitySchemes[*]
  name: siemens-bearer-auth-required
  severity: error
- description: List endpoints should support OData skip/top pagination
  given: $.paths[*].get.parameters[?(@.in == 'query')]
  name: siemens-odata-pagination
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: siemens-operation-summary-required
  severity: error
- description: Equipment type fields should use enumeration
  given: $.components.schemas[*].properties.type
  name: siemens-equipment-type-enum
  severity: warn
- description: Status fields must define enumerated values
  given: $.components.schemas[*].properties.status
  name: siemens-status-enum
  severity: warn
- description: List responses should use OData value array wrapper
  given: $.components.schemas[?(@.properties.value)]
  name: siemens-list-response-value-array
  severity: warn
- description: Timestamp fields must use ISO 8601 date-time format
  given: $.components.schemas[*].properties[?(@.description =~ /timestamp|time|date/i)]
  name: siemens-timestamp-format
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: siemens-operation-id-required
  severity: error
rules_file: rules/siemens-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/siemens/refs/heads/main/rules/siemens-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: siemens-rules
source_filename: siemens-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Siemens Building X APIs use Bearer token auth\n  siemens-bearer-auth-required:\n    description: Siemens Building X APIs must use Bearer token authentication\n    message: API security must include Bearer token scheme\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: scheme\n      function: enumeration\n      functionOptions:\n        values:\n          - bearer\n\n  # Building data follows OData paging conventions (skip/top)\n  siemens-odata-pagination:\n    description: List endpoints should support OData skip/top pagination\n    message: List operation should define skip and top query parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters[?(@.in == 'query')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^(skip|top|filter|select|orderby|from|to|status|type|severity|resolution)$\"\n\n  # All operations must have summary\n  siemens-operation-summary-required:\n\
  \    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Building equipment types should use consistent naming\n  siemens-equipment-type-enum:\n    description: Equipment type fields should use enumeration\n    message: Equipment type should use a defined enumeration\n    severity: warn\n    given: \"$.components.schemas[*].properties.type\"\n    then:\n      field: enum\n      function: truthy\n\n  # Status fields should enumerate valid values\n  siemens-status-enum:\n    description: Status fields must define enumerated values\n    message: Status field should define an enum\n    severity: warn\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  # List responses should use OData value wrapper\n  siemens-list-response-value-array:\n    description: List responses should\
  \ use OData value array wrapper\n    message: List response should wrap results in a 'value' array property\n    severity: warn\n    given: \"$.components.schemas[?(@.properties.value)]\"\n    then:\n      field: properties.value.type\n      function: enumeration\n      functionOptions:\n        values:\n          - array\n\n  # Timestamps must use ISO 8601 format\n  siemens-timestamp-format:\n    description: Timestamp fields must use ISO 8601 date-time format\n    message: \"Timestamp field '{{property}}' should use format: date-time\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.description =~ /timestamp|time|date/i)]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n          - date\n\n  # Operations must have operationId\n  siemens-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n\
  \    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/siemens/refs/heads/main/rules/siemens-rules.yml
tags:
- Automation
- Electrification
- Industry
- Manufacturing
- Building Automation
- Industrial IoT
- Smart Buildings
- Digital Twin
- Spectral
- Linting
- API Governance
---
