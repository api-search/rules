---
api_specs:
- filename: scout-rfp-events-openapi.yml
  format: yaml
  label: Workday Strategic Sourcing API
  slug: workday-strategic-sourcing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scout-rfp/refs/heads/main/openapi/scout-rfp-events-openapi.yml
categories:
- scout
description: Spectral linting rules defining API design standards and conventions for Scout RFP.
layout: rules
name: Scout RFP API Rules
provider_name: Scout RFP
provider_slug: scout-rfp
rule_count: 10
rules:
- description: Responses should use JSON API data wrapper pattern
  given: $.paths[*][*].responses[?(@property >= '200' && @property < '300')].content.application/json.schema
  name: scout-rfp-json-api-data-wrapper
  severity: warn
- description: List endpoints should include pagination metadata
  given: $.paths[*].get.responses[200].content.application/json.schema
  name: scout-rfp-pagination-meta
  severity: warn
- description: All operations must require API key authentication headers
  given: $.paths[*][*]
  name: scout-rfp-api-key-auth
  severity: error
- description: All operations must have operationId
  given: $.paths[*][*]
  name: scout-rfp-operation-ids
  severity: error
- description: API paths should include version prefix
  given: $.paths
  name: scout-rfp-versioned-paths
  severity: info
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: scout-rfp-camel-case-operation-ids
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: scout-rfp-tags-required
  severity: warn
- description: GET list endpoints should support pagination parameters
  given: $.paths[*].get
  name: scout-rfp-pagination-parameters
  severity: info
- description: Document rate limiting constraints
  given: $.info
  name: scout-rfp-rate-limit-documentation
  severity: info
- description: Path parameters for resources should be named 'id'
  given: $.paths[*][*].parameters[?(@.in === 'path')]
  name: scout-rfp-resource-id-path-params
  severity: warn
rules_file: rules/scout-rfp-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scout-rfp/refs/heads/main/rules/scout-rfp-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 5
slug: scout-rfp-rules
source_filename: scout-rfp-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Scout RFP API uses JSON API specification format\n  scout-rfp-json-api-data-wrapper:\n    description: Responses should use JSON API data wrapper pattern\n    message: \"Response schema should include 'data' property following JSON API spec\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '200' && @property < '300')].content.application/json.schema\"\n    then:\n      field: properties.data\n      function: truthy\n\n  scout-rfp-pagination-meta:\n    description: List endpoints should include pagination metadata\n    message: \"List response schemas should include 'meta' property for pagination\"\n    severity: warn\n    given: \"$.paths[*].get.responses[200].content.application/json.schema\"\n    then:\n      field: properties.meta\n      function: truthy\n\n  scout-rfp-api-key-auth:\n    description: All operations must require API key authentication headers\n    message: \"Operations should require X-Api-Key\
  \ security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  scout-rfp-operation-ids:\n    description: All operations must have operationId\n    message: \"Every operation must have a unique operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  scout-rfp-versioned-paths:\n    description: API paths should include version prefix\n    message: \"API paths should start with /services/ or include version\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(services|v[0-9]+)/\"\n\n  scout-rfp-camel-case-operation-ids:\n    description: Operation IDs should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase naming\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[a-z][a-zA-Z0-9]*$\"\n\n  scout-rfp-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operations must be tagged for proper grouping\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  scout-rfp-pagination-parameters:\n    description: GET list endpoints should support pagination parameters\n    message: \"List endpoints should support page[size] and page parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  scout-rfp-rate-limit-documentation:\n    description: Document rate limiting constraints\n    message: \"API info should document the 5 requests/second rate limit\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  scout-rfp-resource-id-path-params:\n    description: Path parameters for resources should be named 'id'\n    message: \"Resource path parameters\
  \ should follow {id} or {resource_id} naming\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in === 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[a-z_]+id$|^id$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scout-rfp/refs/heads/main/rules/scout-rfp-rules.yml
tags:
- Procurement
- Sourcing
- RFP
- Supply Chain
- Workday
- Spectral
- Linting
- API Governance
---
