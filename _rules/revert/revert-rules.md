---
api_specs:
- filename: revert-unified-api-openapi.yml
  format: yaml
  label: Revert Unified API
  slug: revert-unified-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/revert/refs/heads/main/openapi/revert-unified-api-openapi.yml
categories:
- revert
description: Spectral linting rules defining API design standards and conventions for Revert.
layout: rules
name: Revert API Rules
provider_name: Revert
provider_slug: revert
rule_count: 10
rules:
- description: All operationIds must use camelCase format consistent with Revert SDK generation
  given: $.paths.*.*
  name: revert-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: revert-tags-title-case
  severity: warn
- description: All endpoints except /connection must include x-revert-t-id header
  given: $.paths[?(!@property.match(/^\/connection$/))].*
  name: revert-tenant-id-header-required
  severity: error
- description: All endpoints must declare x-revert-api-token security
  given: $.paths.*.*
  name: revert-api-token-auth
  severity: error
- description: All 200 responses should include a status field in the schema
  given: $.paths.*.*.responses.200.content.application/json.schema.properties
  name: revert-response-status-field
  severity: warn
- description: List endpoints returning paginated results must include next and previous cursor fields
  given: $.paths[?(@property.match(/^(?!.*\{id\}).*$/))].get.responses.200.content.application/json.schema.properties
  name: revert-pagination-cursor-consistency
  severity: warn
- description: All API paths should follow the established /crm/, /ticket/, /chat/, /accounting/ namespace pattern
  given: $.paths
  name: revert-version-prefix
  severity: info
- description: API paths must not end with a trailing slash
  given: $.paths
  name: revert-no-trailing-slash
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: revert-kebab-case-paths
  severity: warn
- description: Request bodies for create/update operations should include an additional field for non-unified data
  given: $.paths.*.post.requestBody.content.application/json.schema.properties
  name: revert-additional-fields-support
  severity: info
rules_file: rules/revert-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/revert/refs/heads/main/rules/revert-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 6
slug: revert-rules
source_filename: revert-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  revert-operation-id-camel-case:\n    description: All operationIds must use camelCase format consistent with Revert SDK generation\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  revert-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  revert-tenant-id-header-required:\n    description: All endpoints except /connection must include x-revert-t-id header\n    severity: error\n    given: \"$.paths[?(!@property.match(/^\\\\/connection$/))].*\"\n    then:\n      field: parameters\n      function: truthy\n\n  revert-api-token-auth:\n    description: All endpoints must declare x-revert-api-token security\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field:\
  \ security\n      function: defined\n\n  revert-response-status-field:\n    description: All 200 responses should include a status field in the schema\n    severity: warn\n    given: \"$.paths.*.*.responses.200.content.application/json.schema.properties\"\n    then:\n      field: status\n      function: defined\n\n  revert-pagination-cursor-consistency:\n    description: List endpoints returning paginated results must include next and previous cursor fields\n    severity: warn\n    given: \"$.paths[?(@property.match(/^(?!.*\\\\{id\\\\}).*$/))].get.responses.200.content.application/json.schema.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            next:\n              type: object\n            previous:\n              type: object\n\n  revert-version-prefix:\n    description: All API paths should follow the established /crm/, /ticket/, /chat/, /accounting/ namespace pattern\n    severity: info\n    given: \"$.paths\"\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/connection|\\\\/crm\\\\/|\\\\/ticket\\\\/|\\\\/chat\\\\/|\\\\/accounting\\\\/)\"\n\n  revert-no-trailing-slash:\n    description: API paths must not end with a trailing slash\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  revert-kebab-case-paths:\n    description: Path segments must use kebab-case\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z][a-z0-9-]*)(\\\\/{[^}]+})?(\\\\/[a-z][a-z0-9-]*)*(\\\\/\\\\{[^}]+\\\\})?$\"\n\n  revert-additional-fields-support:\n    description: Request bodies for create/update operations should include an additional field for non-unified data\n    severity: info\n    given: \"$.paths.*.post.requestBody.content.application/json.schema.properties\"\n    then:\n      field: additional\n      function:\
  \ defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/revert/refs/heads/main/rules/revert-rules.yml
tags:
- Integrations
- CRM
- Unified API
- Open Source
- Spectral
- Linting
- API Governance
---
