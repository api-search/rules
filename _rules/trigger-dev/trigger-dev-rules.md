---
api_specs:
- filename: trigger-dev-management-openapi.yml
  format: yaml
  label: Trigger.dev Management API
  slug: trigger-dev-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trigger-dev/refs/heads/main/openapi/trigger-dev-management-openapi.yml
categories:
- trigger
description: Spectral linting rules defining API design standards and conventions for Trigger.dev.
layout: rules
name: Trigger.dev API Rules
provider_name: Trigger.dev
provider_slug: trigger-dev
rule_count: 11
rules:
- description: All operations must have a camelCase operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: trigger-dev-operation-id-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: trigger-dev-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: trigger-dev-operation-tags-required
  severity: warn
- description: Run ID parameters should document the run_ prefix format
  given: $.paths[*][*].parameters[?(@.name == 'runId')]
  name: trigger-dev-run-id-format
  severity: hint
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: trigger-dev-path-params-required
  severity: error
- description: POST operations that create resources should have a request body
  given: $.paths[*].post
  name: trigger-dev-post-request-body
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: trigger-dev-response-200-required
  severity: error
- description: Operations should document 401 unauthorized response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: trigger-dev-response-401-required
  severity: warn
- description: All API paths must be versioned
  given: $.paths[*]~
  name: trigger-dev-versioned-path
  severity: warn
- description: Security scheme must use bearer authentication
  given: $.components.securitySchemes[*]
  name: trigger-dev-bearer-auth
  severity: error
- description: RunStatus must reference the canonical enum
  given: $.components.schemas.Run.properties.status
  name: trigger-dev-run-status-enum
  severity: hint
rules_file: rules/trigger-dev-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trigger-dev/refs/heads/main/rules/trigger-dev-rules.yml
severity_counts:
  error: 4
  hint: 2
  info: 0
  warn: 5
slug: trigger-dev-rules
source_filename: trigger-dev-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All operations must have operationId\n  trigger-dev-operation-id-required:\n    description: All operations must have a camelCase operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationIds must use camelCase\n  trigger-dev-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have tags\n  trigger-dev-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation '{{operationId}}' must have at least one tag\"\n    severity: warn\n    given: \"\
  $.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # Run IDs must be in path params and use run_ prefix pattern\n  trigger-dev-run-id-format:\n    description: Run ID parameters should document the run_ prefix format\n    message: \"runId parameter should document the run_ prefix in description\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.name == 'runId')]\"\n    then:\n      field: description\n      function: truthy\n\n  # All path parameters must be required\n  trigger-dev-path-params-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter must have required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  # POST endpoints that create resources must define request body\n  trigger-dev-post-request-body:\n\
  \    description: POST operations that create resources should have a request body\n    message: \"POST operation '{{operationId}}' should define a requestBody\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Responses must include 200 status code\n  trigger-dev-response-200-required:\n    description: All operations must define a 200 response\n    message: \"Operation is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # Responses should include 401 status code\n  trigger-dev-response-401-required:\n    description: Operations should document 401 unauthorized response\n    message: \"Operation should document 401 response for auth failures\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n\
  \  # API paths must use versioned prefix\n  trigger-dev-versioned-path:\n    description: All API paths must be versioned\n    message: \"Path '{{value}}' must start with /api/v1/ or /api/v3/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[13]/\"\n\n  # Bearer auth scheme must be used\n  trigger-dev-bearer-auth:\n    description: Security scheme must use bearer authentication\n    message: \"Security scheme must use type: http with scheme: bearer\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  # RunStatus enum must be defined consistently\n  trigger-dev-run-status-enum:\n    description: RunStatus must reference the canonical enum\n    message: \"Status properties\
  \ should reference RunStatus schema or define the full enum\"\n    severity: hint\n    given: \"$.components.schemas.Run.properties.status\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trigger-dev/refs/heads/main/rules/trigger-dev-rules.yml
tags:
- Developer-First
- Workflow Automation
- Background Jobs
- TypeScript
- AI Agents
- Open Source
- Spectral
- Linting
- API Governance
---
