---
api_specs:
- filename: reuters-connect-api-openapi.yml
  format: yaml
  label: Reuters Connect API
  slug: reuters-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reuters/refs/heads/main/openapi/reuters-connect-api-openapi.yml
categories:
- reuters
description: Spectral linting rules defining API design standards and conventions for Reuters.
layout: rules
name: Reuters API Rules
provider_name: Reuters
provider_slug: reuters
rule_count: 8
rules:
- description: Operation IDs should use camelCase following Reuters Connect API convention.
  given: $.paths[*][*].operationId
  name: reuters-operation-id-camel-case
  severity: warn
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: reuters-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: reuters-tags-defined
  severity: error
- description: The Reuters Connect API uses token-based authentication via query parameter. All content endpoints must reference the tokenAuth security scheme.
  given: $.paths[?(@property != '/login')][*]
  name: reuters-token-auth
  severity: warn
- description: Reuters Connect API responses use XML content type.
  given: $.paths[*][*].responses[*].content
  name: reuters-xml-response-content
  severity: info
- description: All operations should define 401 and 403 error responses.
  given: $.paths[*][*].responses
  name: reuters-error-responses
  severity: warn
- description: Item list endpoints require a channel parameter.
  given: $.paths['/items'].get.parameters
  name: reuters-channel-param-required
  severity: info
- description: Search endpoint requires a query (q) parameter.
  given: $.paths['/search'].get.parameters
  name: reuters-search-query-param
  severity: error
rules_file: rules/reuters-connect-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reuters/refs/heads/main/rules/reuters-connect-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: reuters-connect-api-rules
source_filename: reuters-connect-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [\"spectral:oas\"]\n\nrules:\n  reuters-operation-id-camel-case:\n    description: Operation IDs should use camelCase following Reuters Connect API convention.\n    message: \"Operation ID '{{value}}' should use camelCase (e.g., listChannels, getItem, searchItems).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  reuters-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  reuters-tags-defined:\n    description: All operations must have at least one tag.\n    message: \"Operation is missing tags.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\
  \n  reuters-token-auth:\n    description: >-\n      The Reuters Connect API uses token-based authentication via query parameter.\n      All content endpoints must reference the tokenAuth security scheme.\n    message: \"Content endpoint should require token authentication.\"\n    severity: warn\n    given: \"$.paths[?(@property != '/login')][*]\"\n    then:\n      field: security\n      function: truthy\n\n  reuters-xml-response-content:\n    description: Reuters Connect API responses use XML content type.\n    message: \"Reuters Connect API responses should use application/xml content type.\"\n    severity: info\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      field: \"application/xml\"\n      function: truthy\n\n  reuters-error-responses:\n    description: All operations should define 401 and 403 error responses.\n    message: \"Operation should define 401 Unauthorized response for token-based auth.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n \
  \   then:\n      field: \"401\"\n      function: truthy\n\n  reuters-channel-param-required:\n    description: Item list endpoints require a channel parameter.\n    message: \"The /items endpoint requires a channel query parameter.\"\n    severity: info\n    given: \"$.paths['/items'].get.parameters\"\n    then:\n      function: truthy\n\n  reuters-search-query-param:\n    description: Search endpoint requires a query (q) parameter.\n    message: \"The /search endpoint requires a 'q' query parameter.\"\n    severity: error\n    given: \"$.paths['/search'].get.parameters\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reuters/refs/heads/main/rules/reuters-connect-api-rules.yml
tags:
- Business
- Finance
- Journalism
- Media
- News
- Wire Service
- Spectral
- Linting
- API Governance
---
