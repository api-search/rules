---
api_specs:
- filename: sorry-status-page-openapi.yml
  format: yaml
  label: Sorry Status Page API
  slug: sorry-status-page-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sorry/refs/heads/main/openapi/sorry-status-page-openapi.yml
categories:
- sorry
description: Spectral linting rules defining API design standards and conventions for Sorry.
layout: rules
name: Sorry API Rules
provider_name: Sorry
provider_slug: sorry
rule_count: 12
rules:
- description: Sorry API uses /pages/{page_id}/... nested resource pattern
  given: $.paths
  name: sorry-nested-resource-pattern
  severity: info
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sorry-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sorry-operation-id-required
  severity: error
- description: OperationId must use camelCase convention
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sorry-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sorry-operation-has-tags
  severity: warn
- description: POST and PATCH operations must define a requestBody
  given: $.paths[*][post,patch]
  name: sorry-post-has-request-body
  severity: error
- description: All operations must document a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sorry-401-response
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: sorry-delete-returns-204
  severity: warn
- description: All tags in the spec must use Title Case
  given: $.tags[*].name
  name: sorry-tags-title-case
  severity: warn
- description: API info should mention rate limiting (10 req/s)
  given: $.info
  name: sorry-rate-limit-documented
  severity: info
- description: Bearer auth security must be defined
  given: $
  name: sorry-security-defined
  severity: error
- description: Successful responses must define a JSON schema
  given: $.paths[*][get,post,patch].responses['200','201'].content['application/json']
  name: sorry-response-schema-defined
  severity: warn
rules_file: rules/sorry-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sorry/refs/heads/main/rules/sorry-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 7
slug: sorry-rules
source_filename: sorry-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sorry API uses nested resource paths - enforce consistent pattern\n  sorry-nested-resource-pattern:\n    description: Sorry API uses /pages/{page_id}/... nested resource pattern\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/pages(/.*)?$\"\n\n  # All operations must have summaries in Title Case\n  sorry-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # All operations must have operationId\n  sorry-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId\
  \ must use camelCase\n  sorry-operation-id-camel-case:\n    description: OperationId must use camelCase convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have tags\n  sorry-operation-has-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # POST operations must have requestBody\n  sorry-post-has-request-body:\n    description: POST and PATCH operations must define a requestBody\n    severity: error\n    given: \"$.paths[*][post,patch]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Must document 401 response\n  sorry-401-response:\n    description: All operations must document a 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    then:\n      field: \"401\"\n      function: defined\n\n  # DELETE operations should return 204\n  sorry-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: defined\n\n  # All tags must be Title Case\n  sorry-tags-title-case:\n    description: All tags in the spec must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # Rate limiting documentation\n  sorry-rate-limit-documented:\n    description: API info should mention rate limiting (10 req/s)\n    severity: info\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  # Security must be defined\n  sorry-security-defined:\n    description: Bearer auth security must be defined\n    severity: error\n    given: \"\
  $\"\n    then:\n      field: security\n      function: defined\n\n  # Response schemas for successful responses\n  sorry-response-schema-defined:\n    description: Successful responses must define a JSON schema\n    severity: warn\n    given: \"$.paths[*][get,post,patch].responses['200','201'].content['application/json']\"\n    then:\n      field: schema\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sorry/refs/heads/main/rules/sorry-rules.yml
tags:
- Status Pages
- Incident Management
- Developer Tools
- Monitoring
- Notifications
- Spectral
- Linting
- API Governance
---
