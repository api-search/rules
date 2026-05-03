---
api_specs:
- filename: uptrace-openapi.yml
  format: yaml
  label: Uptrace API
  slug: uptrace
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uptrace/refs/heads/main/openapi/uptrace-openapi.yml
categories:
- uptrace
description: Spectral linting rules defining API design standards and conventions for Uptrace.
layout: rules
name: Uptrace API Rules
provider_name: Uptrace
provider_slug: uptrace
rule_count: 7
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: uptrace-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: uptrace-path-kebab-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: uptrace-summaries-title-case
  severity: warn
- description: All non-ingestion operations should use BearerAuth or DSNAuth
  given: $.paths[?(!@property.match(/prometheus\/write/))][get,post,put,delete]
  name: uptrace-bearer-auth
  severity: info
- description: DELETE operations must return 204
  given: $.paths[*].delete.responses
  name: uptrace-delete-returns-204
  severity: warn
- description: List and create operations should require projectId
  given: $.paths[*].get
  name: uptrace-project-id-required
  severity: info
- description: API paths should use /api/ prefix
  given: $.paths[*]~
  name: uptrace-api-prefix
  severity: info
rules_file: rules/uptrace-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uptrace/refs/heads/main/rules/uptrace-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 3
  warn: 4
slug: uptrace-rules
source_filename: uptrace-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  uptrace-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  uptrace-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{path}}' must use kebab-case segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  uptrace-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]* ?)+$\"\n\n  uptrace-bearer-auth:\n    description:\
  \ All non-ingestion operations should use BearerAuth or DSNAuth\n    message: \"Operation should use BearerAuth or DSNAuth security\"\n    severity: info\n    given: \"$.paths[?(!@property.match(/prometheus\\\\/write/))][get,post,put,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  uptrace-delete-returns-204:\n    description: DELETE operations must return 204\n    message: \"DELETE should return 204 No Content\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['204']\n\n  uptrace-project-id-required:\n    description: List and create operations should require projectId\n    message: \"Collection endpoint should require projectId parameter\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \n  uptrace-api-prefix:\n    description: API paths should use /api/ prefix\n    message: \"Uptrace API paths should start with /api/\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/.*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uptrace/refs/heads/main/rules/uptrace-rules.yml
tags:
- APM
- Observability
- OpenTelemetry
- Distributed Tracing
- Monitoring
- Spectral
- Linting
- API Governance
---
