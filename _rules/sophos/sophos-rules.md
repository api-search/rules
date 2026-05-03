---
api_specs:
- filename: sophos-central-siem-openapi.yml
  format: yaml
  label: Sophos Central SIEM API
  slug: sophos-central-siem-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sophos/refs/heads/main/openapi/sophos-central-siem-openapi.yml
categories:
- sophos
description: Spectral linting rules defining API design standards and conventions for Sophos.
layout: rules
name: Sophos API Rules
provider_name: Sophos
provider_slug: sophos
rule_count: 10
rules:
- description: All Sophos SIEM operations must require the x-api-key header parameter
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'x-api-key')]
  name: sophos-requires-api-key-header
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sophos-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sophos-operation-has-tags
  severity: warn
- description: Sophos APIs use cursor-based pagination; use 'cursor' query parameter
  given: $.paths[*][get].parameters[?(@.name == 'limit')]
  name: sophos-cursor-pagination
  severity: info
- description: Operations with auth must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sophos-401-response
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sophos-operation-id-required
  severity: error
- description: OperationId must use camelCase convention
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sophos-operation-id-camel-case
  severity: warn
- description: Successful responses must have a schema
  given: $.paths[*][get,post,put,patch,delete].responses['200','201'].content['application/json']
  name: sophos-response-schema-defined
  severity: warn
- description: All tags in the spec must use Title Case
  given: $.tags[*].name
  name: sophos-tags-title-case
  severity: warn
- description: Security must be defined at the global or operation level
  given: $
  name: sophos-security-defined
  severity: error
rules_file: rules/sophos-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sophos/refs/heads/main/rules/sophos-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 6
slug: sophos-rules
source_filename: sophos-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sophos API uses x-api-key header + Bearer token dual auth - enforce both\n  sophos-requires-api-key-header:\n    description: All Sophos SIEM operations must require the x-api-key header parameter\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'x-api-key')]\"\n    then:\n      field: required\n      function: truthy\n\n  # All operations must have summaries in Title Case\n  sophos-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # All operations must have tags\n  sophos-operation-has-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n\
  \      function: truthy\n\n  # Pagination cursor pattern - Sophos uses cursor-based pagination\n  sophos-cursor-pagination:\n    description: Sophos APIs use cursor-based pagination; use 'cursor' query parameter\n    severity: info\n    given: \"$.paths[*][get].parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema.maximum\n      function: defined\n\n  # Operations must have 401 response for missing auth\n  sophos-401-response:\n    description: Operations with auth must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  # Operations must have operationId\n  sophos-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId must use camelCase\n  sophos-operation-id-camel-case:\n\
  \    description: OperationId must use camelCase convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Response schemas must be defined\n  sophos-response-schema-defined:\n    description: Successful responses must have a schema\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses['200','201'].content['application/json']\"\n    then:\n      field: schema\n      function: defined\n\n  # All tags must be Title Case\n  sophos-tags-title-case:\n    description: All tags in the spec must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # Security must be defined at global or operation level\n  sophos-security-defined:\n    description: Security must be defined at the global\
  \ or operation level\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sophos/refs/heads/main/rules/sophos-rules.yml
tags:
- Cybersecurity
- Endpoint Protection
- Security
- SIEM
- Threat Detection
- Incident Response
- Spectral
- Linting
- API Governance
---
