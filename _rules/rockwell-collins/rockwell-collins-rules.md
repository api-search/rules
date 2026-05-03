---
api_specs:
- filename: flightaware-aeroapi-openapi.yml
  format: yaml
  label: FlightAware AeroAPI
  slug: flightaware-aeroapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rockwell-collins/refs/heads/main/openapi/flightaware-aeroapi-openapi.yml
categories:
- aeroapi
description: Spectral linting rules defining API design standards and conventions for Rockwell Collins.
layout: rules
name: Rockwell Collins API Rules
provider_name: Rockwell Collins
provider_slug: rockwell-collins
rule_count: 11
rules:
- description: All AeroAPI operations must define security with ApiKeyAuth
  given: $.paths[*][get,post,put,patch,delete]
  name: aeroapi-has-security
  severity: error
- description: All AeroAPI operations must have a unique operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: aeroapi-operation-id-required
  severity: error
- description: AeroAPI operationIds use snake_case naming
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: aeroapi-operation-id-snake-case
  severity: warn
- description: All AeroAPI operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: aeroapi-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: aeroapi-summary-title-case
  severity: warn
- description: AeroAPI operations should include detailed descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: aeroapi-operation-description-required
  severity: warn
- description: Operation tags must use AeroAPI defined categories
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: aeroapi-valid-tag
  severity: warn
- description: List operations should support cursor-based pagination
  given: $.paths[*][get]
  name: aeroapi-pagination-cursor
  severity: info
- description: AeroAPI paths use lowercase with forward slashes
  given: $.paths[*]~
  name: aeroapi-path-format
  severity: warn
- description: Successful responses must include a schema
  given: $.paths[*][get,post,put,patch,delete].responses['200']
  name: aeroapi-success-response-schema
  severity: error
- description: API info must include version
  given: $.info
  name: aeroapi-info-version
  severity: error
rules_file: rules/rockwell-collins-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rockwell-collins/refs/heads/main/rules/rockwell-collins-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 5
slug: rockwell-collins-rules
source_filename: rockwell-collins-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # FlightAware AeroAPI uses x-apikey header authentication\n  aeroapi-has-security:\n    description: All AeroAPI operations must define security with ApiKeyAuth\n    message: \"Operation must include the ApiKeyAuth security scheme (x-apikey header)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # Operations must have operationIds\n  aeroapi-operation-id-required:\n    description: All AeroAPI operations must have a unique operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # OperationIds use snake_case (AeroAPI convention)\n  aeroapi-operation-id-snake-case:\n    description: AeroAPI operationIds use snake_case naming\n    message: \"OperationId '{{value}}' should use snake_case format\"\n    severity:\
  \ warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # Summaries must exist and use Title Case\n  aeroapi-summary-required:\n    description: All AeroAPI operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  aeroapi-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operations must have descriptions\n  aeroapi-operation-description-required:\n    description: AeroAPI operations should include detailed descriptions\n    message: \"Operation is missing\
  \ a description - AeroAPI documentation standard requires detailed descriptions\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Tags must be one of the defined AeroAPI categories\n  aeroapi-valid-tag:\n    description: Operation tags must use AeroAPI defined categories\n    message: \"Tag must be one of: flights, foresight, airports, operators, alerts, history, miscellaneous\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - flights\n          - foresight\n          - airports\n          - operators\n          - alerts\n          - history\n          - miscellaneous\n\n  # Pagination parameters: max_pages and cursor are standard\n  aeroapi-pagination-cursor:\n    description: List operations should support cursor-based pagination\n    message: \"List operations should\
  \ include cursor pagination parameter\"\n    severity: info\n    given: \"$.paths[*][get]\"\n    then:\n      function: defined\n\n  # Path format: all lowercase with slashes\n  aeroapi-path-format:\n    description: AeroAPI paths use lowercase with forward slashes\n    message: \"Path must use lowercase letters and forward slashes\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_/-]+)+$\"\n\n  # 200 responses should have content schemas\n  aeroapi-success-response-schema:\n    description: Successful responses must include a schema\n    message: \"200 response should include content with schema\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses['200']\"\n    then:\n      field: content\n      function: truthy\n\n  # API info must be complete\n  aeroapi-info-version:\n    description: API info must include version\n    message: \"API must define a version number\"\
  \n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rockwell-collins/refs/heads/main/rules/rockwell-collins-rules.yml
tags:
- Avionics
- Aerospace
- Defense
- Aviation
- Flight Deck
- Spectral
- Linting
- API Governance
---
