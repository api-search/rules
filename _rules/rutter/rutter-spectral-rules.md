---
api_specs:
- filename: rutter-unified-api-openapi.yml
  format: yaml
  label: Rutter Unified API
  slug: unified-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rutter/refs/heads/main/openapi/rutter-unified-api-openapi.yml
categories:
- rutter
description: Spectral linting rules defining API design standards and conventions for Rutter.
layout: rules
name: Rutter API Rules
provider_name: Rutter
provider_slug: rutter
rule_count: 8
rules:
- description: All Rutter API requests must include the X-Rutter-Version header
  given: $.paths[*][get,post,put,patch,delete]
  name: rutter-version-header-required
  severity: warn
- description: Most Rutter API operations require an access_token query parameter
  given: $.paths[*][get]
  name: rutter-access-token-required
  severity: warn
- description: All Rutter operationIds should use camelCase
  given: $.paths[*][*].operationId
  name: rutter-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: rutter-tags-title-case
  severity: warn
- description: All operations must have a 200 success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: rutter-response-200-required
  severity: error
- description: List operations should support cursor-based pagination
  given: $.paths[*].get
  name: rutter-pagination-cursor
  severity: info
- description: POST operations that create resources should document Idempotency-Key header
  given: $.paths[*].post
  name: rutter-idempotency-key-on-writes
  severity: info
- description: The API must document Basic auth security scheme
  given: $.components.securitySchemes
  name: rutter-basic-auth-documented
  severity: error
rules_file: rules/rutter-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rutter/refs/heads/main/rules/rutter-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: rutter-spectral-rules
source_filename: rutter-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rutter-version-header-required:\n    description: All Rutter API requests must include the X-Rutter-Version header\n    message: \"Operation '{{description}}' should document the X-Rutter-Version header parameter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: X-Rutter-Version\n              in:\n                const: header\n\n  rutter-access-token-required:\n    description: Most Rutter API operations require an access_token query parameter\n    message: \"Operation '{{description}}' that reads platform data should have access_token parameter\"\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: parameters\n      function: truthy\n\n  rutter-operation-id-camel-case:\n\
  \    description: All Rutter operationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase naming\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rutter-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  rutter-response-200-required:\n    description: All operations must have a 200 success response\n    message: \"Operation '{{description}}' is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"\
  200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  rutter-pagination-cursor:\n    description: List operations should support cursor-based pagination\n    message: \"List operation '{{description}}' should support cursor pagination\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  rutter-idempotency-key-on-writes:\n    description: POST operations that create resources should document Idempotency-Key header\n    message: \"Create operation '{{description}}' should document the Idempotency-Key header\"\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  rutter-basic-auth-documented:\n    description: The API must document Basic auth security scheme\n    message: \"API must define basicAuth security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: basicAuth\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rutter/refs/heads/main/rules/rutter-spectral-rules.yml
tags:
- Accounting
- B2B
- Commerce
- Financial Data
- Payments
- Unified API
- Spectral
- Linting
- API Governance
---
