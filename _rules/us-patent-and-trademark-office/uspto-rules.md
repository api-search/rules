---
api_specs:
- filename: swagger.yaml
  format: yaml
  label: USPTO Open Data Portal API
  slug: open-data-portal-api
  spec_type: OpenAPI
  url: https://data.uspto.gov/swagger/swagger.yaml
- filename: uspto-tsdr-openapi.yml
  format: yaml
  label: USPTO Trademark Status and Document Retrieval API
  slug: tsdr-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-patent-and-trademark-office/refs/heads/main/openapi/uspto-tsdr-openapi.yml
categories:
- uspto
description: Spectral linting rules defining API design standards and conventions for US Patent and Trademark Office.
layout: rules
name: US Patent and Trademark Office API Rules
provider_name: US Patent and Trademark Office
provider_slug: us-patent-and-trademark-office
rule_count: 8
rules:
- description: All USPTO ODP paths must start with /api/v{n}/ prefix
  given: $.paths[*]~
  name: uspto-path-api-version-prefix
  severity: warn
- description: OperationIds should use camelCase convention
  given: $.paths[*][*].operationId
  name: uspto-operation-id-camel-case
  severity: warn
- description: USPTO APIs require API key authentication via X-API-KEY header
  given: $.paths[*][*]
  name: uspto-api-key-security
  severity: warn
- description: Search operations should support start/rows pagination parameters
  given: $.paths[?(@property.match(//search$/))].post
  name: uspto-search-pagination
  severity: info
- description: All operations must have a summary
  given: $.paths[*][*]
  name: uspto-operation-summary-required
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: uspto-get-200-response
  severity: error
- description: Operations must have at least one tag
  given: $.paths[*][*]
  name: uspto-operation-tags
  severity: warn
- description: Path parameters must have description and required=true
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: uspto-path-params-documented
  severity: warn
rules_file: rules/uspto-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-patent-and-trademark-office/refs/heads/main/rules/uspto-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: uspto-rules
source_filename: uspto-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  # USPTO-specific path conventions\n  uspto-path-api-version-prefix:\n    description: All USPTO ODP paths must start with /api/v{n}/ prefix\n    message: \"Path '{{property}}' must begin with /api/v1/ or /api/v2/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+/\"\n\n  # USPTO operation IDs must be camelCase\n  uspto-operation-id-camel-case:\n    description: OperationIds should use camelCase convention\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # API key security must be in place\n  uspto-api-key-security:\n    description: USPTO APIs require API key authentication via X-API-KEY header\n    message: \"Operations should reference the ApiKeyAuth security scheme\"\n\
  \    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - not:\n                required: [\"security\"]\n\n  # Pagination parameters should be present for search operations\n  uspto-search-pagination:\n    description: Search operations should support start/rows pagination parameters\n    message: \"POST search operations should document pagination in request body\"\n    severity: info\n    given: \"$.paths[?(@property.match(/\\/search$/))].post\"\n    then:\n      function: truthy\n\n  # All paths should have operation summaries\n  uspto-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation at '{{path}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Response 200 required for all GET operations\n  uspto-get-200-response:\n\
  \    description: All GET operations must define a 200 response\n    message: \"GET operation at '{{path}}' missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  # Tags must be defined\n  uspto-operation-tags:\n    description: Operations must have at least one tag\n    message: \"Operation at '{{path}}' has no tags\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Path parameters must be documented\n  uspto-path-params-documented:\n    description: Path parameters must have description and required=true\n    message: \"Path parameter '{{property}}' missing description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-patent-and-trademark-office/refs/heads/main/rules/uspto-rules.yml
tags:
- Federal Government
- Patents
- Trademarks
- Intellectual Property
- Open Data
- Spectral
- Linting
- API Governance
---
