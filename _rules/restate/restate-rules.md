---
api_specs:
- filename: restate-admin-api.yml
  format: yaml
  label: Restate Admin API
  slug: restate-admin
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/restate/refs/heads/main/openapi/restate-admin-api.yml
categories:
- restate
description: Spectral linting rules defining API design standards and conventions for Restate.
layout: rules
name: Restate API Rules
provider_name: Restate
provider_slug: restate
rule_count: 10
rules:
- description: Operation IDs must use snake_case (Restate convention)
  given: $.paths[*][*].operationId
  name: restate-operation-ids-snake-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: restate-tags-defined
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: restate-summary-title-case
  severity: warn
- description: All operations must define error responses
  given: $.paths[*][get,post,put,delete,patch]
  name: restate-error-responses-defined
  severity: warn
- description: Create deployment must require URI field
  given: $.paths['/deployments'].post.requestBody.content.application/json.schema
  name: restate-deployment-uri-required
  severity: error
- description: Restate Admin API default server should be on port 9070
  given: $.servers[*].url
  name: restate-server-port-9070
  severity: info
- description: Invocation status must use defined enum values
  given: $.components.schemas.*.properties.status.enum
  name: restate-invocation-status-enum
  severity: error
- description: Paths must not have trailing slashes
  given: $.paths
  name: restate-paths-no-trailing-slash
  severity: error
- description: Success responses should reference schemas
  given: $.paths[*][*].responses[200,201].content.application/json
  name: restate-response-schemas-defined
  severity: warn
- description: API version should follow semver format
  given: $.info.version
  name: restate-info-version-semver
  severity: warn
rules_file: rules/restate-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/restate/refs/heads/main/rules/restate-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 6
slug: restate-rules
source_filename: restate-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Restate Admin API conventions\n  restate-operation-ids-snake-case:\n    description: Operation IDs must use snake_case (Restate convention)\n    message: \"Operation ID '{{value}}' must use snake_case\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  restate-tags-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  restate-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  restate-error-responses-defined:\n\
  \    description: All operations must define error responses\n    message: \"Operation must define error response codes (400, 404, or 500)\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n              anyOf:\n                - required: [\"400\"]\n                - required: [\"404\"]\n                - required: [\"500\"]\n\n  restate-deployment-uri-required:\n    description: Create deployment must require URI field\n    message: \"Deployment registration request must require 'uri' field\"\n    severity: error\n    given: \"$.paths['/deployments'].post.requestBody.content.application/json.schema\"\n    then:\n      field: required\n      function: defined\n\n  restate-server-port-9070:\n    description: Restate Admin API default server should be on port 9070\n    message: \"Admin API\
  \ server URL should reference port 9070\"\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(localhost:9070|\\\\{baseUrl\\\\})\"\n\n  restate-invocation-status-enum:\n    description: Invocation status must use defined enum values\n    message: \"Invocation status must be one of the defined enum values\"\n    severity: error\n    given: \"$.components.schemas.*.properties.status.enum\"\n    then:\n      function: defined\n\n  restate-paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: \"Path '{{path}}' must not have a trailing slash\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  restate-response-schemas-defined:\n    description: Success responses should reference schemas\n    message: \"200/201 response must define a schema\"\n    severity: warn\n    given: \"$.paths[*][*].responses[200,201].content.application/json\"\
  \n    then:\n      field: schema\n      function: defined\n\n  restate-info-version-semver:\n    description: API version should follow semver format\n    message: \"API version '{{value}}' should follow semver (e.g., 1.4.0)\"\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\d+\\\\.\\\\d+\\\\.\\\\d+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/restate/refs/heads/main/rules/restate-rules.yml
tags:
- Durable Execution
- Workflows
- Microservices
- Orchestration
- Distributed Systems
- Spectral
- Linting
- API Governance
---
