---
api_specs:
- filename: trino-client-api-openapi.yml
  format: yaml
  label: Trino Client REST API
  slug: trino-client-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trino/refs/heads/main/openapi/trino-client-api-openapi.yml
categories:
- trino
description: Spectral linting rules defining API design standards and conventions for Trino.
layout: rules
name: Trino API Rules
provider_name: Trino
provider_slug: trino
rule_count: 8
rules:
- description: All Trino API paths must be versioned with /v1/ prefix
  given: $.paths[*]~
  name: trino-path-must-start-with-v1
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trino-operation-summary-title-case
  severity: warn
- description: Operations should document the X-Trino-User header
  given: $.paths[*].post.parameters[*]
  name: trino-user-header-documented
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: trino-operation-id-camel-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: trino-operation-must-have-description
  severity: warn
- description: GET operations must have a 200 response defined
  given: $.paths[*].get
  name: trino-get-must-have-200
  severity: error
- description: Path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path')].description
  name: trino-path-params-must-have-descriptions
  severity: warn
- description: Schema names must use PascalCase
  given: $.components.schemas[*]~
  name: trino-schema-names-pascal-case
  severity: warn
rules_file: rules/trino-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trino/refs/heads/main/rules/trino-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: trino-rules
source_filename: trino-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Trino uses versioned paths: /v1/...\n  trino-path-must-start-with-v1:\n    description: All Trino API paths must be versioned with /v1/ prefix\n    message: \"Path '{{property}}' must start with /v1/\"\n    given: \"$.paths[*]~\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  # All operation summaries must use Title Case\n  trino-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Trino client API requires X-Trino-User header documentation\n  trino-user-header-documented:\n    description: Operations should document the X-Trino-User header\n    message: \"Trino operations should include X-Trino-User header parameter\"\n\
  \    given: \"$.paths[*].post.parameters[*]\"\n    severity: warn\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - X-Trino-User\n\n  # operationIds must be camelCase\n  trino-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' should be camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have descriptions\n  trino-operation-must-have-description:\n    description: All operations must have a description\n    message: \"Operation at '{{path}}' is missing a description\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # Responses must include a 200 for GET operations\n  trino-get-must-have-200:\n    description: GET operations must have a 200 response\
  \ defined\n    message: \"GET operation is missing a 200 response\"\n    given: \"$.paths[*].get\"\n    severity: error\n    then:\n      field: responses.200\n      function: truthy\n\n  # Path parameters must have descriptions\n  trino-path-params-must-have-descriptions:\n    description: Path parameters must have descriptions\n    message: \"Path parameter '{{value}}' is missing a description\"\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')].description\"\n    severity: warn\n    then:\n      function: truthy\n\n  # Components/schemas must use PascalCase\n  trino-schema-names-pascal-case:\n    description: Schema names must use PascalCase\n    message: \"Schema '{{property}}' should use PascalCase\"\n    given: \"$.components.schemas[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trino/refs/heads/main/rules/trino-rules.yml
tags:
- Analytics
- Big Data
- Distributed SQL
- MySQL
- NoSQL
- Queries
- SQL
- Spectral
- Linting
- API Governance
---
