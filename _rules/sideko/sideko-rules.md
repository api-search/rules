---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Sideko API
  slug: sideko-api
  spec_type: OpenAPI
  url: https://docs.sideko.dev/reference/
categories:
- sideko
description: Spectral linting rules defining API design standards and conventions for Sideko.
layout: rules
name: Sideko API Rules
provider_name: Sideko
provider_slug: sideko
rule_count: 10
rules:
- description: Resource identifiers must use UUID format
  given: $.components.schemas[*].properties[?(@.description =~ /identifier|id/i)]
  name: sideko-id-format-uuid
  severity: warn
- description: List response schemas must include items array and total count
  given: $.components.schemas[?(@.properties.items && @.type == 'object')]
  name: sideko-list-response-shape
  severity: warn
- description: SDK language must be from the supported language list
  given: $.components.schemas[?(@.properties.language)].properties.language
  name: sideko-sdk-language-enum
  severity: error
- description: Status fields should use enumeration
  given: $.components.schemas[*].properties.status
  name: sideko-status-enum
  severity: warn
- description: Resource creation endpoints should return HTTP 201
  given: $.paths[*].post.responses
  name: sideko-create-returns-201
  severity: warn
- description: Delete operations should return HTTP 204 No Content
  given: $.paths[*].delete.responses
  name: sideko-delete-returns-204
  severity: warn
- description: API key header must use x-sideko-key
  given: $.components.securitySchemes[?(@.type == 'apiKey')].name
  name: sideko-api-key-header-name
  severity: error
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: sideko-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: sideko-operation-summary-required
  severity: error
- description: Path parameters should use $ref to components/parameters
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: sideko-path-params-use-refs
  severity: hint
rules_file: rules/sideko-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sideko/refs/heads/main/rules/sideko-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: sideko-rules
source_filename: sideko-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sideko API uses UUID format for all resource identifiers\n  sideko-id-format-uuid:\n    description: Resource identifiers must use UUID format\n    message: \"The '{{property}}' field should use format: uuid\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.description =~ /identifier|id/i)]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - uuid\n\n  # All list endpoints must return an items array and total count\n  sideko-list-response-shape:\n    description: List response schemas must include items array and total count\n    message: List response schemas should have items (array) and total (integer) properties\n    severity: warn\n    given: \"$.components.schemas[?(@.properties.items && @.type == 'object')]\"\n    then:\n      field: properties.total\n      function: truthy\n\n  # SDK language values must be from the approved enumeration\n  sideko-sdk-language-enum:\n\
  \    description: SDK language must be from the supported language list\n    message: SDK language must be one of python, typescript, java, go, ruby, or rust\n    severity: error\n    given: \"$.components.schemas[?(@.properties.language)].properties.language\"\n    then:\n      field: enum\n      function: truthy\n\n  # Status fields must use consistent enumeration patterns\n  sideko-status-enum:\n    description: Status fields should use enumeration\n    message: \"Status field '{{property}}' should define an enum\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  # All POST endpoints for resource creation should return 201\n  sideko-create-returns-201:\n    description: Resource creation endpoints should return HTTP 201\n    message: POST operations creating resources should define a 201 response\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n    \
  \  function: truthy\n\n  # All DELETE operations should return 204 No Content\n  sideko-delete-returns-204:\n    description: Delete operations should return HTTP 204 No Content\n    message: DELETE operations should define a 204 response\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  # Authentication header must use x-sideko-key convention\n  sideko-api-key-header-name:\n    description: API key header must use x-sideko-key\n    message: API key authentication must use the header name x-sideko-key\n    severity: error\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - x-sideko-key\n\n  # Operation IDs must use camelCase\n  sideko-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., listApiProjects,\
  \ createApiKey)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have a summary\n  sideko-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Path parameters must be referenced in components/parameters\n  sideko-path-params-use-refs:\n    description: Path parameters should use $ref to components/parameters\n    message: Path parameters should reference shared parameter definitions\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: $ref\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sideko/refs/heads/main/rules/sideko-rules.yml
tags:
- CLI
- Documentation
- Mock Servers
- Platform
- SDKs
- API Tooling
- SDK Generation
- Spectral
- Linting
- API Governance
---
