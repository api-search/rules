---
api_specs:
- filename: rely-openapi.yml
  format: yaml
  label: Rely.io Public API
  slug: public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rely/refs/heads/main/openapi/rely-openapi.yml
categories:
- rely
description: Spectral linting rules defining API design standards and conventions for Rely.io.
layout: rules
name: Rely.io API Rules
provider_name: Rely.io
provider_slug: rely
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: rely-operation-ids-camel-case
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: rely-summary-title-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: rely-tags-required
  severity: error
- description: API must define Bearer authentication
  given: $.components.securitySchemes
  name: rely-bearer-auth
  severity: error
- description: All paths must begin with /api/v1/
  given: $.paths
  name: rely-api-path-prefix
  severity: error
- description: Successful GET responses must have a schema
  given: $.paths[*].get.responses[200].content.application/json
  name: rely-crud-response-schemas
  severity: warn
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: rely-delete-204
  severity: warn
- description: POST operations must have a requestBody
  given: $.paths[*].post
  name: rely-post-request-body
  severity: error
- description: Resource ID path parameters should use {id} naming pattern
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: rely-path-ids-in-path
  severity: warn
- description: All protected operations must define a 401 response
  given: $.paths[*][*].responses
  name: rely-401-on-all-operations
  severity: error
rules_file: rules/rely-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rely/refs/heads/main/rules/rely-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 4
slug: rely-rules
source_filename: rely-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rely-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rely-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 -]*$\"\n\n  rely-tags-required:\n    description: Every operation must have at least one tag\n    message: Operation must include at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  rely-bearer-auth:\n    description: API must define Bearer authentication\n    message: API must use Bearer token authentication\n\
  \    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  rely-api-path-prefix:\n    description: All paths must begin with /api/v1/\n    message: \"Path '{{property}}' must start with /api/v1/\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v1/\"\n\n  rely-crud-response-schemas:\n    description: Successful GET responses must have a schema\n    message: GET 200 responses must define a content schema\n    severity: warn\n    given: \"$.paths[*].get.responses[200].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  rely-delete-204:\n    description: DELETE operations should return 204\n    message: DELETE operations should return a 204 No Content response\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  rely-post-request-body:\n\
  \    description: POST operations must have a requestBody\n    message: POST operations must define a requestBody\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  rely-path-ids-in-path:\n    description: Resource ID path parameters should use {id} naming pattern\n    message: Path ID parameters should follow consistent naming (blueprintId, entityId, etc.)\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z]*Id$\"\n\n  rely-401-on-all-operations:\n    description: All protected operations must define a 401 response\n    message: Operation must define a 401 Unauthorized response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rely/refs/heads/main/rules/rely-rules.yml
tags:
- Developer Experience
- Internal Developer Portal
- Platform Engineering
- Software Catalog
- Service Catalog
- Engineering Scorecards
- Spectral
- Linting
- API Governance
---
