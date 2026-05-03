---
api_specs:
- filename: trello-rest-api-openapi.yml
  format: yaml
  label: Trello REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trello/refs/heads/main/openapi/trello-rest-api-openapi.yml
- filename: trello-webhooks-asyncapi.yml
  format: yaml
  label: Trello Webhooks API
  slug: webhooks-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/trello/refs/heads/main/asyncapi/trello-webhooks-asyncapi.yml
categories:
- trello
description: Spectral linting rules defining API design standards and conventions for trello.
layout: rules
name: trello API Rules
provider_name: trello
provider_slug: trello
rule_count: 11
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: trello-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trello-summary-title-case
  severity: warn
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: trello-security-defined
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: trello-response-200-get
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: trello-tag-defined
  severity: warn
- description: Trello uses API key and token query parameter authentication
  given: $.components.securitySchemes
  name: trello-api-key-auth
  severity: info
- description: API paths should use kebab-case
  given: $.paths[*]~
  name: trello-path-kebab-case
  severity: warn
- description: Operations with request bodies should define a 400 response
  given: $.paths[*][post,put,patch]
  name: trello-response-400-defined
  severity: warn
- description: DELETE operations should return 200 or 204
  given: $.paths[*].delete
  name: trello-delete-response
  severity: warn
- description: POST operations that create resources should define a request body
  given: $.paths[*].post
  name: trello-post-request-body
  severity: warn
- description: Query string parameters must not appear in path definitions
  given: $.paths[*]~
  name: trello-no-query-strings-in-path
  severity: error
rules_file: rules/trello-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trello/refs/heads/main/rules/trello-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 7
slug: trello-spectral-rules
source_filename: trello-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  trello-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trello-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /()+&-]*$\"\n\n  trello-security-defined:\n    description: All operations must define security requirements\n    message: \"Operation must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  trello-response-200-get:\n    description: All GET operations\
  \ must define a 200 response\n    message: \"GET operation must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  trello-tag-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  trello-api-key-auth:\n    description: Trello uses API key and token query parameter authentication\n    message: \"Trello auth uses apiKey and token query parameters\"\n    severity: info\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  trello-path-kebab-case:\n    description: API paths should use kebab-case\n    message: \"Path should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n       \
  \ match: \"^(/[a-z0-9][a-z0-9-]*(/[a-z0-9][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)+$\"\n\n  trello-response-400-defined:\n    description: Operations with request bodies should define a 400 response\n    message: \"POST/PUT/PATCH operation should define 400 Bad Request\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch]\"\n    then:\n      field: responses.400\n      function: defined\n\n  trello-delete-response:\n    description: DELETE operations should return 200 or 204\n    message: \"DELETE operation should define a success response\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      function: defined\n\n  trello-post-request-body:\n    description: POST operations that create resources should define a request body\n    message: \"POST operation should include a requestBody\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  trello-no-query-strings-in-path:\n    description:\
  \ Query string parameters must not appear in path definitions\n    message: \"Path must not contain query strings\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trello/refs/heads/main/rules/trello-spectral-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
