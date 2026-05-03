---
api_specs:
- filename: retool-management-api-openapi.yml
  format: yaml
  label: Retool Management API
  slug: retool-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/retool/refs/heads/main/openapi/retool-management-api-openapi.yml
categories:
- retool
description: Spectral linting rules defining API design standards and conventions for Retool.
layout: rules
name: Retool API Rules
provider_name: Retool
provider_slug: retool
rule_count: 9
rules:
- description: Operation IDs should use camelCase following the Retool API convention.
  given: $.paths[*][*].operationId
  name: retool-operation-id-camel-case
  severity: warn
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: retool-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag for grouping in the API reference.
  given: $.paths[*][*]
  name: retool-tags-defined
  severity: error
- description: Successful GET responses must include a response schema.
  given: $.paths[*].get.responses.200
  name: retool-response-200-schema
  severity: warn
- description: POST and PUT operations must include a request body.
  given: $.paths[*][post,put]
  name: retool-request-body-post-put
  severity: error
- description: Operations should document 401 and 403 error responses.
  given: $.paths[*][get,post,put,delete].responses
  name: retool-error-responses
  severity: warn
- description: User ID path parameters should be named 'userId' and use UUID format.
  given: $.paths[*][*].parameters[?(@.in == 'path' && @.name == 'id')]
  name: retool-uuid-path-params
  severity: hint
- description: The Retool API uses Bearer token authentication exclusively.
  given: $.components.securitySchemes[*]
  name: retool-bearer-auth-scheme
  severity: error
- description: List endpoints returning collections should support page and pageSize parameters.
  given: $.paths[*].get
  name: retool-pagination-parameters
  severity: hint
rules_file: rules/retool-management-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/retool/refs/heads/main/rules/retool-management-api-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 4
slug: retool-management-api-rules
source_filename: retool-management-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [\"spectral:oas\"]\n\nrules:\n  retool-operation-id-camel-case:\n    description: Operation IDs should use camelCase following the Retool API convention.\n    message: \"Operation ID '{{value}}' should use camelCase (e.g., listUsers, createUser, deleteApp).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  retool-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case (capitalize each significant word).\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  retool-tags-defined:\n    description: All operations must have at least one tag for grouping in the API reference.\n    message: \"Operation is missing tags. Add at least one tag from the defined\
  \ tags list.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  retool-response-200-schema:\n    description: Successful GET responses must include a response schema.\n    message: \"GET operation '{{path}}' should define a response schema for 200 OK.\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  retool-request-body-post-put:\n    description: POST and PUT operations must include a request body.\n    message: \"POST/PUT operation must define a requestBody.\"\n    severity: error\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  retool-error-responses:\n    description: Operations should document 401 and 403 error responses.\n    message: \"Operation should define 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].responses\"\n    then:\n      field:\
  \ \"401\"\n      function: truthy\n\n  retool-uuid-path-params:\n    description: User ID path parameters should be named 'userId' and use UUID format.\n    message: \"User ID parameter should be named 'userId' with uuid format.\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.in == 'path' && @.name == 'id')]\"\n    then:\n      function: falsy\n\n  retool-bearer-auth-scheme:\n    description: The Retool API uses Bearer token authentication exclusively.\n    message: \"Security scheme should use Bearer token (http, bearer).\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  const: bearer\n\n  retool-pagination-parameters:\n    description: List endpoints returning collections should support page and pageSize parameters.\n    message: \"\
  List endpoint (GET returning array) should define pagination parameters.\"\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/retool/refs/heads/main/rules/retool-management-api-rules.yml
tags:
- Admin Panel
- Dashboard
- Internal Tools
- Low Code
- No Code
- Spectral
- Linting
- API Governance
---
