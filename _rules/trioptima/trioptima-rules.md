---
api_specs:
- filename: trioptima-trireduce-api-openapi.yml
  format: yaml
  label: Trioptima triReduce API
  slug: trireduce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trioptima/refs/heads/main/openapi/trioptima-trireduce-api-openapi.yml
categories:
- trioptima
description: Spectral linting rules defining API design standards and conventions for Trioptima.
layout: rules
name: Trioptima API Rules
provider_name: Trioptima
provider_slug: trioptima
rule_count: 7
rules:
- description: All triReduce API paths must start with /api/v1/ or /v1/
  given: $.paths[*]~
  name: trioptima-path-api-versioned
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: trioptima-operation-must-have-id
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trioptima-summary-title-case
  severity: warn
- description: POST and PUT operations should have a requestBody defined
  given: $.paths[*][post,put]
  name: trioptima-mutation-must-have-body
  severity: warn
- description: All operations must reference an OAuth 2.0 security scheme
  given: $.paths[*][get,post,put,patch,delete]
  name: trioptima-operation-must-be-secured
  severity: warn
- description: Schema component names must use PascalCase
  given: $.components.schemas[*]~
  name: trioptima-schema-names-pascal-case
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: trioptima-must-have-401-response
  severity: warn
rules_file: rules/trioptima-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trioptima/refs/heads/main/rules/trioptima-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: trioptima-rules
source_filename: trioptima-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # triReduce API paths must use /api/v1/ prefix\n  trioptima-path-api-versioned:\n    description: All triReduce API paths must start with /api/v1/ or /v1/\n    message: \"Path '{{property}}' must start with /api/v1/ or /v1/\"\n    given: \"$.paths[*]~\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(api/v1|v1)/\"\n\n  # All operations must have operationIds\n  trioptima-operation-must-have-id:\n    description: All operations must have an operationId\n    message: \"Operation at '{{path}}' is missing an operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  # Operation summaries must use Title Case\n  trioptima-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][*].summary\"\n   \
  \ severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # POST/PUT operations must have request body\n  trioptima-mutation-must-have-body:\n    description: POST and PUT operations should have a requestBody defined\n    message: \"POST/PUT operation at '{{path}}' is missing a requestBody\"\n    given: \"$.paths[*][post,put]\"\n    severity: warn\n    then:\n      field: requestBody\n      function: truthy\n\n  # Security must be defined for all operations (authenticated API)\n  trioptima-operation-must-be-secured:\n    description: All operations must reference an OAuth 2.0 security scheme\n    message: \"Operation at '{{path}}' must define security requirements\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - properties: {}\n\n  # Schema names must\
  \ use PascalCase\n  trioptima-schema-names-pascal-case:\n    description: Schema component names must use PascalCase\n    message: \"Schema '{{property}}' should use PascalCase\"\n    given: \"$.components.schemas[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]+$\"\n\n  # All operations must have 401 response defined\n  trioptima-must-have-401-response:\n    description: All operations must document 401 Unauthorized response\n    message: \"Operation is missing 401 response definition\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    severity: warn\n    then:\n      field: \"401\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trioptima/refs/heads/main/rules/trioptima-rules.yml
tags:
- CME Group
- Derivatives
- Financial Services
- OSTTRA
- Portfolio Compression
- Post-Trade Services
- Reconciliation
- Risk Management
- Spectral
- Linting
- API Governance
---
