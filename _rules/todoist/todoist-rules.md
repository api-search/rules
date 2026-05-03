---
api_specs:
- filename: todoist-openapi.yml
  format: yaml
  label: Todoist API
  slug: todoist-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/todoist/refs/heads/main/openapi/todoist-openapi.yml
categories:
- todoist
description: Spectral linting rules defining API design standards and conventions for Todoist.
layout: rules
name: Todoist API Rules
provider_name: Todoist
provider_slug: todoist
rule_count: 10
rules:
- description: Todoist uses POST for update operations, not PUT/PATCH
  given: $.paths.*.put
  name: todoist-post-for-updates
  severity: warn
- description: OperationIds must use camelCase format
  given: $.paths[*][*].operationId
  name: todoist-operation-id-camelcase
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: todoist-path-kebab-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: todoist-operation-id-required
  severity: error
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: todoist-tags-required
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: todoist-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: todoist-summary-title-case
  severity: warn
- description: API must use Bearer token authentication
  given: $.components.securitySchemes
  name: todoist-auth-bearer
  severity: error
- description: Operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: todoist-success-response
  severity: warn
- description: Path parameters must be defined in operation parameters
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]
  name: todoist-path-params-defined
  severity: error
rules_file: rules/todoist-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/todoist/refs/heads/main/rules/todoist-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: todoist-rules
source_filename: todoist-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Todoist API uses POST for updates (not PUT/PATCH)\n  todoist-post-for-updates:\n    description: Todoist uses POST for update operations, not PUT/PATCH\n    message: Update operations should use POST method, not PUT or PATCH\n    severity: warn\n    given: \"$.paths.*.put\"\n    then:\n      function: undefined\n\n  # All operation IDs should use camelCase\n  todoist-operation-id-camelcase:\n    description: OperationIds must use camelCase format\n    message: \"{{property}} operationId should be camelCase (e.g., createTask, getProject)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Paths should use kebab-case\n  todoist-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment {{value}} should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}/]*)+$\"\n\n  # All operations must have an operationId\n  todoist-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # All operations must have tags\n  todoist-tags-required:\n    description: All operations must be tagged\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # All operations must have a summary\n  todoist-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Summaries must\
  \ use Title Case\n  todoist-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"{{value}} summary should be in Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ()-]*$\"\n\n  # Bearer token authentication required\n  todoist-auth-bearer:\n    description: API must use Bearer token authentication\n    message: Security scheme must be bearerAuth type\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  # Responses should include 200 for success\n  todoist-success-response:\n    description: Operations must define a success response\n    message: Operation should define a 200, 201, or 204 success response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # Path parameters must be defined in parameters\n  todoist-path-params-defined:\n    description: Path parameters must be defined in operation parameters\n    message: Path parameter must be defined in parameters array\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/todoist/refs/heads/main/rules/todoist-rules.yml
tags:
- Productivity
- Tasks
- To-Do
- Task Management
- Collaboration
- Spectral
- Linting
- API Governance
---
