---
api_specs:
- filename: toornament-openapi.yml
  format: yaml
  label: Toornament Organizer API
  slug: organizer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toornament/refs/heads/main/openapi/toornament-openapi.yml
categories:
- toornament
description: Spectral linting rules defining API design standards and conventions for Toornament.
layout: rules
name: Toornament API Rules
provider_name: Toornament
provider_slug: toornament
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: toornament-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: toornament-operation-id-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: toornament-operation-description-required
  severity: warn
- description: API key security should be defined
  given: $.components.securitySchemes
  name: toornament-api-key-required
  severity: error
- description: OAuth2 security should be defined for write operations
  given: $.components.securitySchemes
  name: toornament-oauth2-required
  severity: error
- description: List endpoints (GET /tournaments etc.) should document Range header
  given: $.paths[*].get.parameters[?(@.name == 'Range')]
  name: toornament-pagination-range-header
  severity: warn
- description: Paginated list endpoints should return 206 Partial Content
  given: $.paths[*].get.responses
  name: toornament-list-response-206
  severity: hint
- description: Path parameters should have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: toornament-path-param-description
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: toornament-delete-no-content
  severity: warn
rules_file: rules/toornament-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toornament/refs/heads/main/rules/toornament-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 5
slug: toornament-rules
source_filename: toornament-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n  # Toornament API uses Title Case operation summaries\n  toornament-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  # All operations must have operationId\n  toornament-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # All operations must have a description\n  toornament-operation-description-required:\n    description: All operations must have a description\n    message: \"Operation is missing a description\"\n    severity: warn\n\
  \    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Tournament endpoints must require X-Api-Key header\n  toornament-api-key-required:\n    description: API key security should be defined\n    message: \"X-Api-Key security scheme should be defined\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: apiKey\n      function: truthy\n\n  # OAuth2 security scheme should be defined\n  toornament-oauth2-required:\n    description: OAuth2 security should be defined for write operations\n    message: \"OAuth2 security scheme should be defined\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: oauth2\n      function: truthy\n\n  # Paginated list endpoints should accept Range header\n  toornament-pagination-range-header:\n    description: List endpoints (GET /tournaments etc.) should document Range header\n    message: \"Paginated GET endpoints should\
  \ accept a Range header parameter\"\n    severity: warn\n    given: \"$.paths[*].get.parameters[?(@.name == 'Range')]\"\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values:\n          - header\n\n  # Successful list responses should return 206 Partial Content\n  toornament-list-response-206:\n    description: Paginated list endpoints should return 206 Partial Content\n    message: \"Paginated list endpoint should return 206, not 200\"\n    severity: hint\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"206\"\n      function: truthy\n\n  # Path parameters should be described\n  toornament-path-param-description:\n    description: Path parameters should have descriptions\n    message: \"Path parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n\n  # DELETE operations should return 204\n  toornament-delete-no-content:\n\
  \    description: DELETE operations should return 204 No Content\n    message: \"DELETE operation should include a 204 response\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toornament/refs/heads/main/rules/toornament-rules.yml
tags:
- Esports
- Gaming
- Tournaments
- Brackets
- Competition
- Spectral
- Linting
- API Governance
---
