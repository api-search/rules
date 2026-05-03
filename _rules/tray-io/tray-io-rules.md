---
api_specs:
- filename: tray-io-platform-api-openapi.yml
  format: yaml
  label: Tray.io Platform API
  slug: tray-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tray-io/refs/heads/main/openapi/tray-io-platform-api-openapi.yml
categories:
- tray
description: Spectral linting rules defining API design standards and conventions for Tray.io.
layout: rules
name: Tray.io API Rules
provider_name: Tray.io
provider_slug: tray-io
rule_count: 6
rules:
- description: Operation IDs should use camelCase naming convention consistent with Tray.io API conventions (e.g., listConnectors, callConnector).
  given: $.paths[*][*].operationId
  name: tray-io-operation-id-camel-case
  severity: warn
- description: All Tray.io API endpoints require Bearer token authentication.
  given: $.paths[*][*]
  name: tray-io-bearer-auth-required
  severity: error
- description: All operations should define a successful response (200 or 204).
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tray-io-response-success-defined
  severity: warn
- description: All Tray.io operations should document the 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tray-io-401-defined
  severity: warn
- description: All operations should include a description.
  given: $.paths[*][*]
  name: tray-io-description-required
  severity: warn
- description: All operations should have at least one tag.
  given: $.paths[*][*].tags
  name: tray-io-tags-required
  severity: warn
rules_file: rules/tray-io-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tray-io/refs/heads/main/rules/tray-io-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 5
slug: tray-io-rules
source_filename: tray-io-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tray-io-operation-id-camel-case:\n    description: >-\n      Operation IDs should use camelCase naming convention consistent with\n      Tray.io API conventions (e.g., listConnectors, callConnector).\n    message: \"Operation ID '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tray-io-bearer-auth-required:\n    description: >-\n      All Tray.io API endpoints require Bearer token authentication.\n    message: \"All operations require Bearer token authentication\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - not:\n                required: [\"security\"]\n\n  tray-io-response-success-defined:\n    description: >-\n      All operations should\
  \ define a successful response (200 or 204).\n    message: \"Operation should define a 200 or 204 success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"204\"]\n\n  tray-io-401-defined:\n    description: All Tray.io operations should document the 401 Unauthorized response.\n    message: \"Operation should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  tray-io-description-required:\n    description: All operations should include a description.\n    message: \"Operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\
  \n  tray-io-tags-required:\n    description: All operations should have at least one tag.\n    message: \"Operation should have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tray-io/refs/heads/main/rules/tray-io-rules.yml
tags:
- AI Agents
- API Aggregation
- Automation
- Connectors
- Integration
- iPaaS
- Workflow Automation
- Spectral
- Linting
- API Governance
---
