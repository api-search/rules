---
api_specs:
- filename: wegowise-openapi.yml
  format: yaml
  label: WegoWise API
  slug: wegowise
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wegowise/refs/heads/main/openapi/wegowise-openapi.yml
categories:
- wegowise
description: Spectral linting rules defining API design standards and conventions for WegoWise.
layout: rules
name: WegoWise API Rules
provider_name: WegoWise
provider_slug: wegowise
rule_count: 12
rules:
- description: Path parameters named 'id' should be typed as integer
  given: $.paths[*][*].parameters[?(@.name == 'id')]
  name: wegowise-path-id-integer
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: wegowise-operation-id-required
  severity: error
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: wegowise-operation-id-camel-case
  severity: warn
- description: Operation summaries must start with a capital letter (Title Case)
  given: $.paths[*][*].summary
  name: wegowise-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: wegowise-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: wegowise-operation-tags
  severity: warn
- description: Date query parameters should specify format date
  given: $.paths[*][*].parameters[?(@.name == 'start_date' || @.name == 'end_date')]
  name: wegowise-date-parameter-format
  severity: warn
- description: data_type parameters should define valid enum values
  given: $.paths[*][*].parameters[?(@.name == 'data_type')]
  name: wegowise-data-type-enum
  severity: warn
- description: Authenticated operations must define a 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wegowise-401-response
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: wegowise-delete-204
  severity: warn
- description: POST create operations should return 201 Created
  given: $.paths[*].post.responses
  name: wegowise-post-201
  severity: info
- description: Component schemas must have descriptions
  given: $.components.schemas[*]
  name: wegowise-schema-description
  severity: warn
rules_file: rules/wegowise-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wegowise/refs/heads/main/rules/wegowise-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 10
slug: wegowise-rules
source_filename: wegowise-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # WegoWise uses integer IDs in paths\n  wegowise-path-id-integer:\n    description: Path parameters named 'id' should be typed as integer\n    message: Path parameter 'id' should have type integer in {{path}}\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'id')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  # All operations must have operationId\n  wegowise-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId must be camelCase\n  wegowise-operation-id-camel-case:\n    description: operationId must use camelCase\n    message: operationId \"{{value}}\" must be camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries must use Title Case\n  wegowise-summary-title-case:\n    description: Operation summaries must start with a capital letter (Title Case)\n    message: Summary \"{{value}}\" must start with a capital letter\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operations must have a description\n  wegowise-description-required:\n    description: All operations must have a description\n    message: Operation is missing a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # All operations should have tags\n  wegowise-operation-tags:\n    description: All operations must have at least one tag\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # Date parameters should use ISO 8601 format\n  wegowise-date-parameter-format:\n    description: Date query parameters should specify format date\n    message: Date parameter \"{{value}}\" should have format 'date'\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'start_date' || @.name == 'end_date')]\"\n    then:\n      field: schema.format\n      function: truthy\n\n  # Enum parameters should have enum values\n  wegowise-data-type-enum:\n    description: data_type parameters should define valid enum values\n    message: data_type parameter should define enum values\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'data_type')]\"\n    then:\n      field: schema.enum\n      function: truthy\n\n  # Responses must define 401 for authenticated endpoints\n  wegowise-401-response:\n    description: Authenticated operations must define a 401 response\n    message: Operation is missing a 401\
  \ response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # DELETE operations should return 204\n  wegowise-delete-204:\n    description: DELETE operations should return 204 No Content\n    message: DELETE operation should define a 204 response\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  # POST operations should return 201\n  wegowise-post-201:\n    description: POST create operations should return 201 Created\n    message: POST operation should define a 201 response\n    severity: info\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  # Schemas must have descriptions\n  wegowise-schema-description:\n    description: Component schemas must have descriptions\n    message: Schema \"{{path}}\" is missing a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\
  \n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wegowise/refs/heads/main/rules/wegowise-rules.yml
tags:
- Benchmarking
- Building Energy
- Energy Efficiency
- Multifamily
- Property Management
- Utility Data
- Spectral
- Linting
- API Governance
---
