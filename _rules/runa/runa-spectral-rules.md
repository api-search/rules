---
api_specs:
- filename: runa-payouts-api-openapi.yml
  format: yaml
  label: Runa Payouts API
  slug: runa-payouts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runa/refs/heads/main/openapi/runa-payouts-api-openapi.yml
categories:
- runa
description: Spectral linting rules defining API design standards and conventions for Runa.
layout: rules
name: Runa API Rules
provider_name: Runa
provider_slug: runa
rule_count: 9
rules:
- description: All operationIds must use camelCase naming convention.
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: runa-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: runa-tags-title-case
  severity: warn
- description: All operations must use X-Api-Key apiKey authentication.
  given: $.components.securitySchemes.apiKeyAuth
  name: runa-api-key-header
  severity: warn
- description: Order creation endpoint should document X-Idempotency-Key header.
  given: $.paths.*.post.parameters[?(@.name=='X-Idempotency-Key')]
  name: runa-idempotency-key-on-orders
  severity: warn
- description: All path segments must use kebab-case.
  given: $.paths
  name: runa-paths-kebab-case
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: runa-response-200-defined
  severity: error
- description: All secured endpoints must define a 401 response.
  given: $.paths.*[get,post].responses
  name: runa-401-defined
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: runa-summaries-title-case
  severity: warn
- description: API version should be expressed in the server URL path.
  given: $.servers[*].url
  name: runa-versioned-api
  severity: info
rules_file: rules/runa-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/runa/refs/heads/main/rules/runa-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 7
slug: runa-spectral-rules
source_filename: runa-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  runa-operation-ids-camel-case:\n    description: All operationIds must use camelCase naming convention.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  runa-tags-title-case:\n    description: All tags must use Title Case.\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  runa-api-key-header:\n    description: All operations must use X-Api-Key apiKey authentication.\n    severity: warn\n    given: \"$.components.securitySchemes.apiKeyAuth\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            name:\n              const: X-Api-Key\n\n  runa-idempotency-key-on-orders:\n    description: Order creation endpoint should document X-Idempotency-Key header.\n    severity:\
  \ warn\n    given: \"$.paths.*.post.parameters[?(@.name=='X-Idempotency-Key')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            in:\n              const: header\n\n  runa-paths-kebab-case:\n    description: All path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  runa-response-200-defined:\n    description: All operations must define a 200 response.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - \"200\"\n\n  runa-401-defined:\n    description: All secured endpoints must define a 401 response.\n    severity: warn\n    given: \"$.paths.*[get,post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n\
  \            - \"401\"\n\n  runa-summaries-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  runa-versioned-api:\n    description: API version should be expressed in the server URL path.\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/runa/refs/heads/main/rules/runa-spectral-rules.yml
tags:
- Gift Cards
- Rewards
- Payments
- Incentives
- Payouts
- Spectral
- Linting
- API Governance
---
