---
api_specs:
- filename: singlestore-data-api-openapi.yml
  format: yaml
  label: SingleStore Data API
  slug: data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/singlestore/refs/heads/main/openapi/singlestore-data-api-openapi.yml
- filename: singlestore-management-api-openapi.yml
  format: yaml
  label: SingleStore Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/singlestore/refs/heads/main/openapi/singlestore-management-api-openapi.yml
categories:
- singlestore
description: Spectral linting rules defining API design standards and conventions for SingleStore.
layout: rules
name: SingleStore API Rules
provider_name: SingleStore
provider_slug: singlestore
rule_count: 8
rules:
- description: All SingleStore API operations must use Bearer token authentication
  given: $.paths.*.*.security
  name: singlestore-bearer-auth
  severity: error
- description: All operation summaries must use Title Case
  given: $.paths.*.*.summary
  name: singlestore-title-case-summaries
  severity: warn
- description: All operationId values must use camelCase
  given: $.paths.*.*.operationId
  name: singlestore-camel-case-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: singlestore-tags-required
  severity: warn
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: singlestore-https-servers
  severity: error
- description: All operations should define error response codes
  given: $.paths.*.*
  name: singlestore-error-responses
  severity: warn
- description: API info must include contact information
  given: $.info
  name: singlestore-contact-info
  severity: warn
- description: API should include external documentation link
  given: $
  name: singlestore-external-docs
  severity: info
rules_file: rules/singlestore-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/singlestore/refs/heads/main/rules/singlestore-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: singlestore-rules
source_filename: singlestore-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  singlestore-bearer-auth:\n    description: All SingleStore API operations must use Bearer token authentication\n    message: \"Operation is missing Bearer token security requirement\"\n    severity: error\n    given: \"$.paths.*.*.security\"\n    then:\n      function: truthy\n\n  singlestore-title-case-summaries:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  singlestore-camel-case-operation-ids:\n    description: All operationId values must use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: error\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  singlestore-tags-required:\n    description: All operations must\
  \ have at least one tag\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  singlestore-https-servers:\n    description: All server URLs must use HTTPS\n    message: \"Server URL '{{value}}' must use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  singlestore-error-responses:\n    description: All operations should define error response codes\n    message: \"Operation should define at least a 4xx or 5xx response\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: responses\n      function: truthy\n\n  singlestore-contact-info:\n    description: API info must include contact information\n    message: \"API info is missing contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  singlestore-external-docs:\n\
  \    description: API should include external documentation link\n    message: \"API is missing externalDocs reference\"\n    severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/singlestore/refs/heads/main/rules/singlestore-rules.yml
tags:
- Database
- SQL
- Analytics
- Cloud
- Distributed SQL
- Spectral
- Linting
- API Governance
---
