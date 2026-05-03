---
api_specs:
- filename: upkeep-openapi.yml
  format: yaml
  label: UpKeep API
  slug: upkeep
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/upkeep/refs/heads/main/openapi/upkeep-openapi.yml
categories:
- upkeep
description: Spectral linting rules defining API design standards and conventions for UpKeep.
layout: rules
name: UpKeep API Rules
provider_name: UpKeep
provider_slug: upkeep
rule_count: 7
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: upkeep-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: upkeep-path-kebab-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: upkeep-summaries-title-case
  severity: warn
- description: Successful responses should include a success boolean field
  given: $.paths[*][*].responses.200.content.application/json.schema
  name: upkeep-success-envelope
  severity: info
- description: DELETE operations must return 204 No Content
  given: $.paths[*].delete.responses
  name: upkeep-delete-returns-204
  severity: warn
- description: List operations should support page and limit parameters
  given: $.paths[*].get
  name: upkeep-pagination-params
  severity: info
- description: All non-auth operations must require session-token header
  given: $.paths[?(!@property.match(/\/auth/))][get,post,patch,delete]
  name: upkeep-session-token-auth
  severity: warn
rules_file: rules/upkeep-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/upkeep/refs/heads/main/rules/upkeep-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 2
  warn: 5
slug: upkeep-rules
source_filename: upkeep-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  upkeep-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  upkeep-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{path}}' must use kebab-case segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  upkeep-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]* ?)+$\"\n\n  upkeep-success-envelope:\n    description:\
  \ Successful responses should include a success boolean field\n    message: \"Success response should include a 'success' boolean field\"\n    severity: info\n    given: \"$.paths[*][*].responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            properties:\n              type: object\n\n  upkeep-delete-returns-204:\n    description: DELETE operations must return 204 No Content\n    message: \"DELETE operation should return 204\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['204']\n\n  upkeep-pagination-params:\n    description: List operations should support page and limit parameters\n    message: \"List operation should include page and limit query parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n\
  \      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  upkeep-session-token-auth:\n    description: All non-auth operations must require session-token header\n    message: \"Operation must use SessionToken security scheme\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/\\\\/auth/))][get,post,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/upkeep/refs/heads/main/rules/upkeep-rules.yml
tags:
- CMMS
- Maintenance Management
- Asset Management
- Facility Management
- Work Orders
- Spectral
- Linting
- API Governance
---
