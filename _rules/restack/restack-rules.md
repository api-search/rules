---
api_specs:
- filename: restack-openapi.yml
  format: yaml
  label: Restack
  slug: restack
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/restack/refs/heads/main/openapi/restack-openapi.yml
categories:
- restack
description: Spectral linting rules defining API design standards and conventions for Restack.
layout: rules
name: Restack API Rules
provider_name: Restack
provider_slug: restack
rule_count: 10
rules:
- description: Operation IDs must use camelCase (Restack convention)
  given: $.paths[*][*].operationId
  name: restack-operation-ids-kebab-case
  severity: warn
- description: All Restack paths must start with /api/ or /health
  given: $.paths
  name: restack-paths-api-prefix
  severity: warn
- description: Agent and workflow paths must include resource type and name
  given: $.paths
  name: restack-resource-path-components
  severity: info
- description: All non-health endpoints must require bearer authentication
  given: $.paths[?(!@property.match(/health/))][*]
  name: restack-bearer-auth-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: restack-operations-have-tags
  severity: warn
- description: POST operations should have a 200 success response
  given: $.paths[*].post
  name: restack-responses-have-200
  severity: warn
- description: Request bodies must use application/json
  given: $.paths[*][*].requestBody.content
  name: restack-request-body-content-type
  severity: error
- description: Request bodies should wrap input in an 'input' property
  given: $.paths[?(@property.match(/\/api\/(agents|workflows)/)].post.requestBody.content.application/json.schema.properties
  name: restack-input-object-structure
  severity: info
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: restack-summary-title-case
  severity: warn
- description: API info must include contact information
  given: $.info
  name: restack-info-contact-defined
  severity: warn
rules_file: rules/restack-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/restack/refs/heads/main/rules/restack-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 7
slug: restack-rules
source_filename: restack-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Restack API conventions\n  restack-operation-ids-kebab-case:\n    description: Operation IDs must use camelCase (Restack convention)\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  restack-paths-api-prefix:\n    description: All Restack paths must start with /api/ or /health\n    message: \"Path '{{path}}' must start with /api/ or be a system path (/health)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/|^/health$\"\n\n  restack-resource-path-components:\n    description: Agent and workflow paths must include resource type and name\n    message: \"Restack paths should follow /api/{resourceType}/{resourceName} pattern\"\n    severity: info\n    given: \"$.paths\"\n    then:\n     \
  \ function: pattern\n      functionOptions:\n        match: \"^/api/(agents|workflows)/\\\\{[a-zA-Z]+\\\\}\"\n\n  restack-bearer-auth-required:\n    description: All non-health endpoints must require bearer authentication\n    message: \"Operation should require bearerAuth security scheme\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/health/))][*]\"\n    then:\n      field: security\n      function: defined\n\n  restack-operations-have-tags:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag for grouping\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  restack-responses-have-200:\n    description: POST operations should have a 200 success response\n    message: \"POST operation must define a 200 success response\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.200\n      function: defined\n\n  restack-request-body-content-type:\n\
  \    description: Request bodies must use application/json\n    message: \"Request body must use application/json content type\"\n    severity: error\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - application/json\n\n  restack-input-object-structure:\n    description: Request bodies should wrap input in an 'input' property\n    message: \"Request body schema should include an 'input' property wrapping agent/workflow inputs\"\n    severity: info\n    given: \"$.paths[?(@property.match(/\\\\/api\\\\/(agents|workflows)/)].post.requestBody.content.application/json.schema.properties\"\n    then:\n      field: input\n      function: defined\n\n  restack-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  restack-info-contact-defined:\n    description: API info must include contact information\n    message: \"API info must include a contact object\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/restack/refs/heads/main/rules/restack-rules.yml
tags:
- AI Agents
- Workflows
- Orchestration
- Enterprise
- Python
- Spectral
- Linting
- API Governance
---
