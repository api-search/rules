---
api_specs:
- filename: cwms-data-api-openapi.yml
  format: yaml
  label: CWMS Data API
  slug: cwms-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-army-corps-of-engineers/refs/heads/main/openapi/cwms-data-api-openapi.yml
categories:
- cwms
description: Spectral linting rules defining API design standards and conventions for United States Army Corps of Engineers.
layout: rules
name: United States Army Corps of Engineers API Rules
provider_name: United States Army Corps of Engineers
provider_slug: united-states-army-corps-of-engineers
rule_count: 9
rules:
- description: Office query parameters should document the three-character USACE district code convention
  given: $.paths..parameters[?(@.name == "office")].description
  name: cwms-office-code-documented
  severity: warn
- description: Time series name parameters should reference CWMS identifier format
  given: $.paths..[?(@.name == "name" && @.in == "query")].description
  name: cwms-timeseries-name-format
  severity: warn
- description: Paginated endpoints should document page and page-size parameters
  given: $.paths..get.parameters[?(@.name == "page")]
  name: cwms-pagination-documented
  severity: info
- description: Unit parameters should have clear enum values
  given: $.paths..parameters[?(@.name == "unit")].schema
  name: cwms-unit-enum-values
  severity: warn
- description: Date/time parameters should reference ISO 8601 or epoch milliseconds
  given: $.paths..parameters[?(@.name == "begin" || @.name == "end")].description
  name: cwms-timestamp-format-documented
  severity: warn
- description: All GET responses should reference a schema
  given: $.paths..get.responses.200.content.application/json
  name: cwms-response-schemas-defined
  severity: warn
- description: All operations must have operationIds
  given: $.paths[*][*]
  name: cwms-operation-ids-present
  severity: error
- description: All operations should have at least one tag
  given: $.paths[*][*]
  name: cwms-tags-present
  severity: warn
- description: All operations should have descriptions
  given: $.paths[*][*]
  name: cwms-description-present
  severity: warn
rules_file: rules/cwms-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-army-corps-of-engineers/refs/heads/main/rules/cwms-data-api-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 7
slug: cwms-data-api-rules
source_filename: cwms-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # CWMS-specific naming conventions\n\n  cwms-office-code-documented:\n    description: Office query parameters should document the three-character USACE district code convention\n    message: \"Office parameter description should mention three-character USACE district office code\"\n    severity: warn\n    given: $.paths..parameters[?(@.name == \"office\")].description\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(three.character|district office|office code)\"\n\n  cwms-timeseries-name-format:\n    description: Time series name parameters should reference CWMS identifier format\n    message: \"Time series name parameter should document CWMS identifier format\"\n    severity: warn\n    given: $.paths..[?(@.name == \"name\" && @.in == \"query\")].description\n    then:\n      function: truthy\n\n  cwms-pagination-documented:\n    description: Paginated endpoints should document page and page-size parameters\n\
  \    message: \"Paginated endpoints should include page and page-size parameters\"\n    severity: info\n    given: $.paths..get.parameters[?(@.name == \"page\")]\n    then:\n      field: description\n      function: truthy\n\n  cwms-unit-enum-values:\n    description: Unit parameters should have clear enum values\n    message: \"Unit parameters should specify EN (English) and SI (metric) options\"\n    severity: warn\n    given: $.paths..parameters[?(@.name == \"unit\")].schema\n    then:\n      field: enum\n      function: truthy\n\n  cwms-timestamp-format-documented:\n    description: Date/time parameters should reference ISO 8601 or epoch milliseconds\n    message: \"Date/time parameters should document ISO 8601 format or milliseconds since epoch\"\n    severity: warn\n    given: $.paths..parameters[?(@.name == \"begin\" || @.name == \"end\")].description\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(ISO 8601|milliseconds|epoch)\"\n\n  cwms-response-schemas-defined:\n\
  \    description: All GET responses should reference a schema\n    message: \"{{description}}: GET operation 200 response should define a schema\"\n    severity: warn\n    given: $.paths..get.responses.200.content.application/json\n    then:\n      field: schema\n      function: truthy\n\n  cwms-operation-ids-present:\n    description: All operations must have operationIds\n    message: \"Operation {{path}} must have an operationId\"\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: truthy\n\n  cwms-tags-present:\n    description: All operations should have at least one tag\n    message: \"Operation {{path}} should have at least one tag\"\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: truthy\n\n  cwms-description-present:\n    description: All operations should have descriptions\n    message: \"Operation {{path}} should have a description\"\n    severity: warn\n    given: $.paths[*][*]\n  \
  \  then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-army-corps-of-engineers/refs/heads/main/rules/cwms-data-api-rules.yml
tags:
- Engineering
- Federal Government
- Water Resources
- Hydrology
- Civil Engineering
- Spectral
- Linting
- API Governance
---
