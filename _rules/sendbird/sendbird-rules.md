---
api_specs:
- filename: sendbird-platform-openapi.yml
  format: yaml
  label: Sendbird Platform API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sendbird/refs/heads/main/openapi/sendbird-platform-openapi.yml
categories:
- sendbird
description: Spectral linting rules defining API design standards and conventions for Sendbird.
layout: rules
name: Sendbird API Rules
provider_name: Sendbird
provider_slug: sendbird
rule_count: 9
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sendbird-summary-title-case
  severity: warn
- description: All operations must use Api-Token authentication.
  given: $.paths[*][*]
  name: sendbird-api-token-auth
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: sendbird-server-https
  severity: error
- description: OperationId must be camelCase.
  given: $.paths[*][*].operationId
  name: sendbird-operationid-camelcase
  severity: warn
- description: Operations must have a 200 response.
  given: $.paths[*][get,post,put,patch].responses
  name: sendbird-response-200-defined
  severity: error
- description: Operations must include at least one tag.
  given: $.paths[*][*].tags
  name: sendbird-tags-required
  severity: warn
- description: API must define an Error schema in components.
  given: $.components.schemas
  name: sendbird-error-schema
  severity: warn
- description: API info must include contact information.
  given: $.info
  name: sendbird-info-contact
  severity: warn
- description: Query parameters should use snake_case.
  given: $.paths[*][*].parameters[?(@.in == 'query')].name
  name: sendbird-paths-snake-case-query-params
  severity: info
rules_file: rules/sendbird-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sendbird/refs/heads/main/rules/sendbird-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: sendbird-rules
source_filename: sendbird-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sendbird-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9\\\\s]*$\"\n\n  sendbird-api-token-auth:\n    description: All operations must use Api-Token authentication.\n    message: \"Operation must define security with apiTokenAuth.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  sendbird-server-https:\n    description: All server URLs must use HTTPS.\n    message: \"Server URL must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  sendbird-operationid-camelcase:\n    description: OperationId must be camelCase.\n    message: \"\
  OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sendbird-response-200-defined:\n    description: Operations must have a 200 response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  sendbird-tags-required:\n    description: Operations must include at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  sendbird-error-schema:\n    description: API must define an Error schema in components.\n    message: \"components.schemas must include an Error schema.\"\n    severity: warn\n    given: \"$.components.schemas\"\n    then:\n     \
  \ field: Error\n      function: defined\n\n  sendbird-info-contact:\n    description: API info must include contact information.\n    message: \"API info.contact must be defined.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  sendbird-paths-snake-case-query-params:\n    description: Query parameters should use snake_case.\n    message: \"Query parameter '{{value}}' should use snake_case.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sendbird/refs/heads/main/rules/sendbird-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
