---
api_specs:
- filename: windsurf-enterprise-openapi.yml
  format: yaml
  label: Windsurf Enterprise API
  slug: windsurf-enterprise-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/windsurfrules/refs/heads/main/openapi/windsurf-enterprise-openapi.yml
categories:
- windsurf
description: Spectral linting rules defining API design standards and conventions for Windsurf.
layout: rules
name: Windsurf API Rules
provider_name: Windsurf
provider_slug: windsurfrules
rule_count: 8
rules:
- description: All Windsurf Enterprise API endpoints use POST method
  given: $.paths[*]
  name: windsurf-post-only
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: windsurf-operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][*].operationId
  name: windsurf-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: windsurf-operation-tags-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: windsurf-summary-required
  severity: error
- description: All Windsurf API requests should include service_key in body
  given: $.paths[*].post.requestBody.content['application/json'].schema
  name: windsurf-service-key-in-body
  severity: warn
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: windsurf-schema-descriptions
  severity: warn
- description: POST operations must define a 401 response
  given: $.paths[*].post.responses
  name: windsurf-auth-error-response
  severity: warn
rules_file: rules/windsurf-enterprise-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/windsurfrules/refs/heads/main/rules/windsurf-enterprise-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: windsurf-enterprise-rules
source_filename: windsurf-enterprise-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Windsurf Enterprise API uses POST for all endpoints (RPC-style)\n  windsurf-post-only:\n    description: All Windsurf Enterprise API endpoints use POST method\n    message: \"Windsurf Enterprise API endpoints should use POST method\"\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # All operations must have operationIds in camelCase\n  windsurf-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  windsurf-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Operations must have tags\n  windsurf-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summaries must be present\n  windsurf-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Request bodies must include service_key\n  windsurf-service-key-in-body:\n    description: All Windsurf API requests should include service_key in body\n    message: \"Request body schema should include service_key for authentication\"\n    severity: warn\n    given: \"$.paths[*].post.requestBody.content['application/json'].schema\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # Schemas must have descriptions\n  windsurf-schema-descriptions:\n    description: Schema components should have descriptions\n    message: \"Schema '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Response 401 must be defined for auth-required endpoints\n  windsurf-auth-error-response:\n    description: POST operations must define a 401 response\n    message: \"Operation is missing 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"401\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/windsurfrules/refs/heads/main/rules/windsurf-enterprise-rules.yml
tags:
- AI Agents
- AI Copilot
- Coding Standards
- Developer Workflow
- IDE
- Windsurf
- Spectral
- Linting
- API Governance
---
