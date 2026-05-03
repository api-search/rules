---
api_specs:
- filename: rtx-eagle-api-openapi.yml
  format: yaml
  label: RTX EAGLE API
  slug: eagle-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rtx/refs/heads/main/openapi/rtx-eagle-api-openapi.yml
categories:
- rtx
description: Spectral linting rules defining API design standards and conventions for RTX.
layout: rules
name: RTX API Rules
provider_name: RTX
provider_slug: rtx
rule_count: 6
rules:
- description: All operationIds must use camelCase naming convention.
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: rtx-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: rtx-tags-title-case
  severity: warn
- description: RTX EAGLE API uses bearer token authentication.
  given: $.components.securitySchemes
  name: rtx-bearer-auth-required
  severity: warn
- description: All path segments must use kebab-case.
  given: $.paths
  name: rtx-paths-kebab-case
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: rtx-response-200-defined
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: rtx-summaries-title-case
  severity: warn
rules_file: rules/rtx-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rtx/refs/heads/main/rules/rtx-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 5
slug: rtx-spectral-rules
source_filename: rtx-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rtx-operation-ids-camel-case:\n    description: All operationIds must use camelCase naming convention.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rtx-tags-title-case:\n    description: All tags must use Title Case.\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  rtx-bearer-auth-required:\n    description: RTX EAGLE API uses bearer token authentication.\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            bearerAuth:\n              type: object\n\n  rtx-paths-kebab-case:\n    description: All path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  rtx-response-200-defined:\n    description: All operations must define a 200 response.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - \"200\"\n\n  rtx-summaries-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rtx/refs/heads/main/rules/rtx-spectral-rules.yml
tags:
- Defense
- Aerospace
- Government
- Logistics
- Intelligence
- Military
- Spectral
- Linting
- API Governance
---
