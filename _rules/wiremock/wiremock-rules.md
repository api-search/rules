---
api_specs:
- filename: wiremock-admin-api-openapi.yml
  format: yaml
  label: WireMock Admin API
  slug: wiremock-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wiremock/refs/heads/main/openapi/wiremock-admin-api-openapi.yml
categories:
- wiremock
description: Spectral linting rules defining API design standards and conventions for WireMock.
layout: rules
name: WireMock API Rules
provider_name: WireMock
provider_slug: wiremock
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: wiremock-operation-summary-title-case
  severity: warn
- description: All WireMock admin paths must start with /__admin/.
  given: $.paths
  name: wiremock-admin-path-prefix
  severity: warn
- description: Path parameters representing IDs should use UUID format examples.
  given: $.paths[*].parameters[?(@.in == 'path')]
  name: wiremock-uuid-path-param
  severity: info
- description: All GET operations must define a 200 response.
  given: $.paths[*].get
  name: wiremock-response-200-defined
  severity: warn
- description: All operations should have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: wiremock-operation-tags
  severity: warn
- description: POST/PUT operations that accept a body should specify application/json content type.
  given: $.paths[*][post,put].requestBody.content
  name: wiremock-json-request-body
  severity: warn
- description: Operations should have descriptions when complex behavior is involved.
  given: $.paths[*][post,put,delete]
  name: wiremock-no-empty-descriptions
  severity: info
rules_file: rules/wiremock-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wiremock/refs/heads/main/rules/wiremock-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 2
  warn: 5
slug: wiremock-rules
source_filename: wiremock-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # WireMock Admin API Spectral Rules\n  # These rules enforce conventions specific to the WireMock Admin API\n\n  wiremock-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*( [A-Z a-z]+)*$\"\n\n  wiremock-admin-path-prefix:\n    description: All WireMock admin paths must start with /__admin/.\n    message: \"WireMock admin path '{{property}}' should start with /__admin/.\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/__admin/\"\n\n  wiremock-uuid-path-param:\n    description: Path parameters representing IDs should use UUID format examples.\n    message: \"Path parameter '{{value}}' should\
  \ document UUID format.\"\n    severity: info\n    given: \"$.paths[*].parameters[?(@.in == 'path')]\"\n    then:\n      - field: schema.type\n        function: truthy\n      - field: example\n        function: truthy\n\n  wiremock-response-200-defined:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' should define a 200 response.\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  wiremock-operation-tags:\n    description: All operations should have at least one tag.\n    message: \"Operation is missing tags.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  wiremock-json-request-body:\n    description: POST/PUT operations that accept a body should specify application/json content type.\n    message: \"Request body should specify application/json content type.\"\n    severity:\
  \ warn\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  wiremock-no-empty-descriptions:\n    description: Operations should have descriptions when complex behavior is involved.\n    message: \"Consider adding a description for this operation.\"\n    severity: info\n    given: \"$.paths[*][post,put,delete]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wiremock/refs/heads/main/rules/wiremock-rules.yml
tags:
- API Mocking
- Mock Server
- Mocking
- Platform
- Stubs
- Testing
- Spectral
- Linting
- API Governance
---
