---
api_specs:
- filename: census-data-api-openapi.yml
  format: yaml
  label: Census Data API
  slug: census-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-census-bureau/refs/heads/main/openapi/census-data-api-openapi.yml
categories:
- census
description: Spectral linting rules defining API design standards and conventions for United States Census Bureau.
layout: rules
name: United States Census Bureau API Rules
provider_name: United States Census Bureau
provider_slug: united-states-census-bureau
rule_count: 8
rules:
- description: Year path parameters should document available year ranges
  given: $.paths..parameters[?(@.name == "year")].description
  name: census-year-parameter-documented
  severity: warn
- description: The get query parameter is the primary Census API parameter and should be marked required
  given: $.paths..parameters[?(@.name == "get")]
  name: census-get-parameter-required
  severity: error
- description: The for geography parameter should document FIPS code syntax
  given: $.paths..parameters[?(@.name == "for")].description
  name: census-for-geography-documented
  severity: warn
- description: API key parameters should explain usage limits
  given: $.paths..parameters[?(@.name == "key")].description
  name: census-key-parameter-documented
  severity: info
- description: All operations must have operationIds
  given: $.paths[*][*]
  name: census-operation-ids-present
  severity: error
- description: All operations should have tags for dataset grouping
  given: $.paths[*][*]
  name: census-tags-present
  severity: warn
- description: All 200 responses should define response schema
  given: $.paths..responses.200.content.application/json
  name: census-response-schema-defined
  severity: warn
- description: The 2D array response format should be documented
  given: $.paths..[?(@.tags && @.tags.includes('American Community Survey'))].description
  name: census-2d-array-response-described
  severity: info
rules_file: rules/census-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-census-bureau/refs/heads/main/rules/census-data-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: census-data-api-rules
source_filename: census-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  census-year-parameter-documented:\n    description: Year path parameters should document available year ranges\n    message: \"Year path parameters should document the range of available data years\"\n    severity: warn\n    given: $.paths..parameters[?(@.name == \"year\")].description\n    then:\n      function: truthy\n\n  census-get-parameter-required:\n    description: The get query parameter is the primary Census API parameter and should be marked required\n    message: \"The 'get' query parameter should be required for Census Data API endpoints\"\n    severity: error\n    given: $.paths..parameters[?(@.name == \"get\")]\n    then:\n      field: required\n      function: truthy\n\n  census-for-geography-documented:\n    description: The for geography parameter should document FIPS code syntax\n    message: \"The 'for' parameter should document geography FIPS filter syntax\"\n    severity: warn\n    given: $.paths..parameters[?(@.name\
  \ == \"for\")].description\n    then:\n      function: truthy\n\n  census-key-parameter-documented:\n    description: API key parameters should explain usage limits\n    message: \"The 'key' parameter should describe the usage limits benefit (500+ requests/day)\"\n    severity: info\n    given: $.paths..parameters[?(@.name == \"key\")].description\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(requests|limit|key)\"\n\n  census-operation-ids-present:\n    description: All operations must have operationIds\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: truthy\n\n  census-tags-present:\n    description: All operations should have tags for dataset grouping\n    message: \"Operation should be tagged with its dataset category\"\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: truthy\n\n  census-response-schema-defined:\n\
  \    description: All 200 responses should define response schema\n    message: \"200 response should define the DataAPIResponse or GeocodeResponse schema\"\n    severity: warn\n    given: $.paths..responses.200.content.application/json\n    then:\n      field: schema\n      function: truthy\n\n  census-2d-array-response-described:\n    description: The 2D array response format should be documented\n    message: \"Census 2D array response format should be described in the operation description\"\n    severity: info\n    given: $.paths..[?(@.tags && @.tags.includes('American Community Survey'))].description\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-census-bureau/refs/heads/main/rules/census-data-api-rules.yml
tags:
- Demographics
- Federal Government
- Open Data
- Statistics
- Economics
- Population
- Spectral
- Linting
- API Governance
---
