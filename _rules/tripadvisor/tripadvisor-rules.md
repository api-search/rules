---
api_specs:
- filename: tripadvisor-content-api-openapi.yml
  format: yaml
  label: Tripadvisor Content API
  slug: content-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tripadvisor/refs/heads/main/openapi/tripadvisor-content-api-openapi.yml
- filename: tripadvisor-hotel-availability-check-api-openapi.yml
  format: yaml
  label: Tripadvisor Hotel Availability Check API
  slug: hotel-availability-check-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tripadvisor/refs/heads/main/openapi/tripadvisor-hotel-availability-check-api-openapi.yml
- filename: tripadvisor-hotel-availability-check-api-openapi.yml
  format: yaml
  label: Tripadvisor Hotel Inventory API
  slug: hotel-inventory-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tripadvisor/refs/heads/main/openapi/tripadvisor-hotel-availability-check-api-openapi.yml
categories:
- tripadvisor
description: Spectral linting rules defining API design standards and conventions for Tripadvisor.
layout: rules
name: Tripadvisor API Rules
provider_name: Tripadvisor
provider_slug: tripadvisor
rule_count: 9
rules:
- description: Tripadvisor Content API paths must use /api/v1/ prefix
  given: $.paths[*]~
  name: tripadvisor-path-versioned
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: tripadvisor-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tripadvisor-summary-title-case
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: tripadvisor-get-must-have-200
  severity: error
- description: All operations must document a 400 Bad Request response
  given: $.paths[*][get,post,put,delete].responses
  name: tripadvisor-must-have-400-response
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,delete].responses
  name: tripadvisor-must-have-401-response
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: tripadvisor-operation-must-have-description
  severity: warn
- description: Schema names must use PascalCase
  given: $.components.schemas[*]~
  name: tripadvisor-schema-pascal-case
  severity: warn
- description: Operations should use tags defined in the top-level tags array
  given: $.paths[*][*].tags[*]
  name: tripadvisor-operations-must-use-defined-tags
  severity: warn
rules_file: rules/tripadvisor-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tripadvisor/refs/heads/main/rules/tripadvisor-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 7
slug: tripadvisor-rules
source_filename: tripadvisor-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Content API must use /api/v1/ prefix\n  tripadvisor-path-versioned:\n    description: Tripadvisor Content API paths must use /api/v1/ prefix\n    message: \"Path '{{property}}' should start with /api/v1/\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(api/v1|v[0-9]+)/\"\n\n  # All operations must have operationIds in camelCase\n  tripadvisor-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operation summaries must use Title Case\n  tripadvisor-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][*].summary\"\
  \n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # All GET operations must have a 200 response\n  tripadvisor-get-must-have-200:\n    description: GET operations must define a 200 response\n    message: \"GET operation is missing a 200 response\"\n    given: \"$.paths[*].get\"\n    severity: error\n    then:\n      field: responses.200\n      function: truthy\n\n  # All operations must have a 400 response for error handling\n  tripadvisor-must-have-400-response:\n    description: All operations must document a 400 Bad Request response\n    message: \"Operation is missing 400 response definition\"\n    given: \"$.paths[*][get,post,put,delete].responses\"\n    severity: warn\n    then:\n      field: \"400\"\n      function: truthy\n\n  # All operations must have a 401 response for unauthorized\n  tripadvisor-must-have-401-response:\n    description: All operations must document 401 Unauthorized response\n    message:\
  \ \"Operation is missing 401 response definition\"\n    given: \"$.paths[*][get,post,put,delete].responses\"\n    severity: warn\n    then:\n      field: \"401\"\n      function: truthy\n\n  # All operations must have descriptions\n  tripadvisor-operation-must-have-description:\n    description: All operations must have a description\n    message: \"Operation at '{{path}}' is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # Schema component names must use PascalCase\n  tripadvisor-schema-pascal-case:\n    description: Schema names must use PascalCase\n    message: \"Schema '{{property}}' should use PascalCase\"\n    given: \"$.components.schemas[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]+$\"\n\n  # Tags must be defined in the top-level tags list\n  tripadvisor-operations-must-use-defined-tags:\n\
  \    description: Operations should use tags defined in the top-level tags array\n    message: \"Tag '{{value}}' used in operation but not defined at top level\"\n    given: \"$.paths[*][*].tags[*]\"\n    severity: warn\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tripadvisor/refs/heads/main/rules/tripadvisor-rules.yml
tags:
- Attractions
- Hotels
- Hospitality
- Restaurants
- Reviews
- Travel
- Spectral
- Linting
- API Governance
---
