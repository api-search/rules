---
api_specs:
- filename: secure-code-warrior-portal-openapi.yml
  format: yaml
  label: Secure Code Warrior Portal API
  slug: secure-code-warrior-portal-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/secure-code-warrior/refs/heads/main/openapi/secure-code-warrior-portal-openapi.yml
categories:
- scw
description: Spectral linting rules defining API design standards and conventions for Secure Code Warrior.
layout: rules
name: Secure Code Warrior API Rules
provider_name: Secure Code Warrior
provider_slug: secure-code-warrior
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: scw-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: scw-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: scw-summaries-title-case
  severity: warn
- description: All operations must require X-API-Key authentication
  given: $.paths[*][*]
  name: scw-api-key-auth
  severity: error
- description: List/reporting endpoints should support page parameter
  given: $.paths[*][get].parameters
  name: scw-pagination-support
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*][delete].responses
  name: scw-delete-returns-204
  severity: warn
- description: POST create operations should return 201 Created
  given: $.paths[*][post].responses
  name: scw-post-create-returns-201
  severity: warn
- description: Partial updates should use PATCH not PUT
  given: $.paths[*]
  name: scw-patch-partial-update
  severity: info
- description: Search/filter endpoints should use POST with body filters
  given: $.paths[~/search$][*]
  name: scw-search-endpoints-post
  severity: info
- description: Date parameters should use ISO 8601 format
  given: $.paths[*][*].parameters[?(@.name =~ /date|Date/)].schema
  name: scw-date-params-iso8601
  severity: warn
rules_file: rules/secure-code-warrior-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/secure-code-warrior/refs/heads/main/rules/secure-code-warrior-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 6
slug: secure-code-warrior-rules
source_filename: secure-code-warrior-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  scw-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  scw-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  scw-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  scw-api-key-auth:\n    description: All operations must require X-API-Key authentication\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  scw-pagination-support:\n    description: List/reporting\
  \ endpoints should support page parameter\n    severity: warn\n    given: \"$.paths[*][get].parameters\"\n    then:\n      function: truthy\n\n  scw-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*][delete].responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  scw-post-create-returns-201:\n    description: POST create operations should return 201 Created\n    severity: warn\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  scw-patch-partial-update:\n    description: Partial updates should use PATCH not PUT\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      function: truthy\n\n  scw-search-endpoints-post:\n    description: Search/filter endpoints should use POST with body filters\n    severity: info\n    given: \"$.paths[~/search$][*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"post\"\n\
  \n  scw-date-params-iso8601:\n    description: Date parameters should use ISO 8601 format\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name =~ /date|Date/)].schema\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n          - date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/secure-code-warrior/refs/heads/main/rules/secure-code-warrior-rules.yml
tags:
- Application Security
- Developer Training
- Security Education
- AppSec
- Secure Coding
- DevSecOps
- Spectral
- Linting
- API Governance
---
