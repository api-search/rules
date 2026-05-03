---
api_specs:
- filename: render-openapi.json
  format: json
  label: Render API
  slug: render-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/render/refs/heads/main/openapi/render-openapi.json
categories:
- render
description: Spectral linting rules defining API design standards and conventions for Render.
layout: rules
name: Render API Rules
provider_name: Render
provider_slug: render
rule_count: 7
rules:
- description: Render API operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: render-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: render-tags-title-case
  severity: warn
- description: Render API path segments must use kebab-case or camelCase IDs
  given: $.paths
  name: render-paths-kebab-case
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: render-response-200-exists
  severity: error
- description: Render API uses BearerAuth authentication scheme
  given: $.components.securitySchemes
  name: render-bearer-auth
  severity: error
- description: Resource IDs in paths must use camelCase with Id suffix
  given: $.paths
  name: render-resource-ids-in-path
  severity: hint
- description: List operations should support cursor-based pagination
  given: $.paths[*].get.parameters[*].name
  name: render-pagination-cursor
  severity: hint
rules_file: rules/render-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/render/refs/heads/main/rules/render-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 3
slug: render-rules
source_filename: render-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n\n  render-operation-ids-camel-case:\n    description: Render API operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  render-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &()/-]*$\"\n\n  render-paths-kebab-case:\n    description: Render API path segments must use kebab-case or camelCase IDs\n    message: \"Path '{{value}}' should use kebab-case segments\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^(/[a-z][a-z0-9-]*|/[a-z][a-zA-Z0-9]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*$\"\n\n  render-response-200-exists:\n    description: All operations must define a 200 response\n    message: \"Operation must define a 200 response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  render-bearer-auth:\n    description: Render API uses BearerAuth authentication scheme\n    message: \"API must declare BearerAuth security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: BearerAuth\n\n  render-resource-ids-in-path:\n    description: Resource IDs in paths must use camelCase with Id suffix\n    message: \"Path parameter for resource ID should use camelCase + Id suffix (e.g., {serviceId}, {postgresId})\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9A-Z-]*|/\\\
  \\{[a-z][a-zA-Z0-9]*Id\\\\}|/\\\\{[a-z][a-zA-Z0-9]*\\\\})*$\"\n\n  render-pagination-cursor:\n    description: List operations should support cursor-based pagination\n    message: \"GET list operations should include a cursor or limit parameter\"\n    severity: hint\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - cursor\n          - limit\n          - offset\n          - before\n          - after\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/render/refs/heads/main/rules/render-rules.yml
tags:
- Cloud
- Platform
- Deployment
- Infrastructure
- DevOps
- Web Services
- Databases
- Hosting
- Spectral
- Linting
- API Governance
---
