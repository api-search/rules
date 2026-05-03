---
api_specs:
- filename: tray-ai-embedded-api-openapi.yml
  format: yaml
  label: Tray.ai Embedded API
  slug: embedded-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/openapi/tray-ai-embedded-api-openapi.yml
- filename: tray-ai-platform-api-openapi.yml
  format: yaml
  label: Tray.ai Platform API
  slug: platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/openapi/tray-ai-platform-api-openapi.yml
categories:
- tray
description: Spectral linting rules defining API design standards and conventions for Tray.ai.
layout: rules
name: Tray.ai API Rules
provider_name: Tray.ai
provider_slug: tray-ai
rule_count: 8
rules:
- description: All operation summaries should be prefixed with "Tray.ai" to clearly identify the provider in multi-API environments.
  given: $.paths[*][*].summary
  name: tray-ai-operation-summary-prefix
  severity: warn
- description: Operation IDs should use camelCase naming convention as used throughout the Tray.ai API (e.g., listConnectors, callConnector, createAuthentication).
  given: $.paths[*][*].operationId
  name: tray-ai-operation-id-camel-case
  severity: warn
- description: All Tray.ai API endpoints require Bearer token authentication. Operations must either inherit global security or declare their own bearerAuth security.
  given: $.paths[*][*]
  name: tray-ai-bearer-auth-required
  severity: error
- description: All operations should define a 200 or 204 success response to document the expected output format for Tray.ai API consumers.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tray-ai-response-200-defined
  severity: warn
- description: All Tray.ai operations require authentication. Each operation should document the 401 Unauthorized response for token errors.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tray-ai-401-response-defined
  severity: warn
- description: All operations should include a description field that explains the operation's purpose, token requirements, and any billing implications.
  given: $.paths[*][*]
  name: tray-ai-description-required
  severity: warn
- description: All operations should be tagged to support navigation in developer documentation and API catalog tools.
  given: $.paths[*][*].tags
  name: tray-ai-tags-required
  severity: warn
- description: API paths should not be empty. Each path should contain at least one HTTP method.
  given: $.paths[*]
  name: tray-ai-no-empty-paths
  severity: error
rules_file: rules/tray-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/rules/tray-ai-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: tray-ai-rules
source_filename: tray-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Tray.ai API naming conventions\n  tray-ai-operation-summary-prefix:\n    description: >-\n      All operation summaries should be prefixed with \"Tray.ai\" to clearly\n      identify the provider in multi-API environments.\n    message: \"Operation summary '{{value}}' should start with 'Tray.ai'\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Tray\\\\.ai \"\n\n  tray-ai-operation-id-camel-case:\n    description: >-\n      Operation IDs should use camelCase naming convention as used throughout\n      the Tray.ai API (e.g., listConnectors, callConnector, createAuthentication).\n    message: \"Operation ID '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tray-ai-bearer-auth-required:\n    description: >-\n\
  \      All Tray.ai API endpoints require Bearer token authentication. Operations\n      must either inherit global security or declare their own bearerAuth security.\n    message: \"All operations require Bearer token authentication\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - not:\n                required: [\"security\"]\n\n  tray-ai-response-200-defined:\n    description: >-\n      All operations should define a 200 or 204 success response to document\n      the expected output format for Tray.ai API consumers.\n    message: \"Operation should define a successful response (200 or 204)\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"204\"\
  ]\n\n  tray-ai-401-response-defined:\n    description: >-\n      All Tray.ai operations require authentication. Each operation should\n      document the 401 Unauthorized response for token errors.\n    message: \"Operation should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  tray-ai-description-required:\n    description: >-\n      All operations should include a description field that explains the\n      operation's purpose, token requirements, and any billing implications.\n    message: \"Operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  tray-ai-tags-required:\n    description: >-\n      All operations should be tagged to support navigation in developer\n      documentation and API catalog tools.\n\
  \    message: \"Operation should have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  tray-ai-no-empty-paths:\n    description: >-\n      API paths should not be empty. Each path should contain at least\n      one HTTP method.\n    message: \"Path should define at least one HTTP operation\"\n    severity: error\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tray-ai/refs/heads/main/rules/tray-ai-rules.yml
tags:
- Automation
- Integration
- iPaaS
- Spectral
- Linting
- API Governance
---
