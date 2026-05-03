---
api_specs:
- filename: thesportsdb-openapi.yml
  format: yaml
  label: TheSportsDB API
  slug: thesportsdb
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thesportsdb/refs/heads/main/openapi/thesportsdb-openapi.yml
categories:
- thesportsdb
description: Spectral linting rules defining API design standards and conventions for TheSportsDB.
layout: rules
name: TheSportsDB API Rules
provider_name: TheSportsDB
provider_slug: thesportsdb
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thesportsdb-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: thesportsdb-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: thesportsdb-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: thesportsdb-description-required
  severity: warn
- description: TheSportsDB API paths end in .php per v1 convention.
  given: $.paths[*]~
  name: thesportsdb-php-path-suffix
  severity: info
- description: All GET operations must define a 200 response.
  given: $.paths[*][get].responses
  name: thesportsdb-200-response-required
  severity: error
- description: Search operations should have at least one query parameter.
  given: $.paths[?(@~'search|lookup')][get]
  name: thesportsdb-query-params-for-search
  severity: warn
- description: All 200 responses must define a content schema.
  given: $.paths[*][get].responses[200].content
  name: thesportsdb-response-schema-json
  severity: warn
rules_file: rules/thesportsdb-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thesportsdb/refs/heads/main/rules/thesportsdb-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: thesportsdb-rules
source_filename: thesportsdb-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  thesportsdb-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  thesportsdb-operation-ids-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  thesportsdb-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  thesportsdb-description-required:\n\
  \    description: All operations must have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  thesportsdb-php-path-suffix:\n    description: TheSportsDB API paths end in .php per v1 convention.\n    message: \"Path '{{path}}' should end with .php per TheSportsDB v1 convention.\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\.php$\"\n\n  thesportsdb-200-response-required:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  thesportsdb-query-params-for-search:\n    description: Search operations should have at least one query parameter.\n\
  \    message: \"Search operation at '{{path}}' must have at least one filter parameter.\"\n    severity: warn\n    given: \"$.paths[?(@~'search|lookup')][get]\"\n    then:\n      field: parameters\n      function: truthy\n\n  thesportsdb-response-schema-json:\n    description: All 200 responses must define a content schema.\n    message: \"Response at '{{path}}' must define a content schema.\"\n    severity: warn\n    given: \"$.paths[*][get].responses[200].content\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thesportsdb/refs/heads/main/rules/thesportsdb-rules.yml
tags:
- Sports
- Database
- Free
- Open Data
- Teams
- Players
- Events
- Spectral
- Linting
- API Governance
---
