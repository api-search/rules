---
api_specs:
- filename: tomtom-maps-openapi.yml
  format: yaml
  label: TomTom Maps API
  slug: tomtom-maps-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/openapi/tomtom-maps-openapi.yml
- filename: tomtom-search-openapi.yml
  format: yaml
  label: TomTom Search API
  slug: tomtom-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/openapi/tomtom-search-openapi.yml
- filename: tomtom-routing-openapi.yml
  format: yaml
  label: TomTom Routing API
  slug: tomtom-routing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/openapi/tomtom-routing-openapi.yml
- filename: tomtom-traffic-openapi.yml
  format: yaml
  label: TomTom Traffic API
  slug: tomtom-traffic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/openapi/tomtom-traffic-openapi.yml
categories:
- tomtom
description: Spectral linting rules defining API design standards and conventions for TomTom.
layout: rules
name: TomTom API Rules
provider_name: TomTom
provider_slug: tomtom
rule_count: 8
rules:
- description: All TomTom API operations must use API key authentication
  given: $.components.securitySchemes
  name: tomtom-api-key-required
  severity: error
- description: TomTom API paths must include a version number
  given: $.paths[*]~
  name: tomtom-version-in-path
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: tomtom-operation-id-required
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: tomtom-operation-id-camelcase
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: tomtom-tags-required
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tomtom-summary-title-case
  severity: warn
- description: Response format path parameters must restrict to valid formats
  given: $.paths[*][get,post].parameters[?(@.name == 'contentType' || @.name == 'format' || @.name == 'ext')]
  name: tomtom-content-type-param
  severity: info
- description: Operations must define a 200 success response
  given: $.paths[*][get,post].responses
  name: tomtom-success-response
  severity: warn
rules_file: rules/tomtom-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/rules/tomtom-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: tomtom-rules
source_filename: tomtom-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # TomTom uses API key authentication\n  tomtom-api-key-required:\n    description: All TomTom API operations must use API key authentication\n    message: API key query parameter 'key' must be defined\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  # Version number must be in path\n  tomtom-version-in-path:\n    description: TomTom API paths must include a version number\n    message: Path should include version number (e.g., /routing/{versionNumber}/)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{versionNumber\\\\}.*\"\n\n  # All operations must have operationId\n  tomtom-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field:\
  \ operationId\n      function: defined\n\n  # OperationIds must use camelCase\n  tomtom-operation-id-camelcase:\n    description: OperationIds must use camelCase\n    message: \"{{property}} operationId should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have tags\n  tomtom-tags-required:\n    description: All operations must be tagged\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # Summaries must use Title Case\n  tomtom-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"{{value}} summary should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n      \
  \  match: \"^[A-Z][A-Za-z0-9 ()-]*$\"\n\n  # Content type path parameters must specify format\n  tomtom-content-type-param:\n    description: Response format path parameters must restrict to valid formats\n    message: Content type path parameter should use enum values\n    severity: info\n    given: \"$.paths[*][get,post].parameters[?(@.name == 'contentType' || @.name == 'format' || @.name == 'ext')]\"\n    then:\n      field: schema.enum\n      function: defined\n\n  # Response success codes defined\n  tomtom-success-response:\n    description: Operations must define a 200 success response\n    message: Operation should define a 200 success response\n    severity: warn\n    given: \"$.paths[*][get,post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tomtom/refs/heads/main/rules/tomtom-rules.yml
tags:
- Maps
- Traffic
- Transportation
- Navigation
- Location
- Geospatial
- Routing
- Geocoding
- Spectral
- Linting
- API Governance
---
