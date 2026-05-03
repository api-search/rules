---
api_specs:
- filename: remitian-tax-payment-openapi.yml
  format: yaml
  label: Remitian Tax Payment API
  slug: tax-payment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/openapi/remitian-tax-payment-openapi.yml
categories:
- remitian
description: Spectral linting rules defining API design standards and conventions for Remitian.
layout: rules
name: Remitian API Rules
provider_name: Remitian
provider_slug: remitian
rule_count: 11
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: remitian-operation-ids-camel-case
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: remitian-summary-title-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: remitian-tags-required
  severity: error
- description: API must define Bearer JWT authentication
  given: $.components.securitySchemes
  name: remitian-bearer-auth
  severity: error
- description: All paths must begin with /v1/
  given: $.paths
  name: remitian-v1-path-prefix
  severity: error
- description: Path segments must use kebab-case
  given: $.paths
  name: remitian-path-kebab-case
  severity: warn
- description: Payment status fields should use the canonical enum values
  given: $.components.schemas.*.properties.status.enum
  name: remitian-payment-status-enum
  severity: warn
- description: All protected operations must define a 401 response
  given: $.paths[*][*].responses
  name: remitian-401-on-protected-operations
  severity: error
- description: POST operations must define a requestBody
  given: $.paths[*].post
  name: remitian-post-request-body-required
  severity: error
- description: List endpoints should support pagination parameters
  given: $.paths[?(!/@id)].get
  name: remitian-pagination-on-list-endpoints
  severity: warn
- description: Schemas should use $ref to components where available
  given: $.paths[*][*].responses[*].content.application/json
  name: remitian-component-refs-used
  severity: info
rules_file: rules/remitian-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/rules/remitian-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 4
slug: remitian-rules
source_filename: remitian-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  remitian-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  remitian-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 -]*$\"\n\n  remitian-tags-required:\n    description: Every operation must have at least one tag\n    message: Operation must include at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  remitian-bearer-auth:\n    description: API must define Bearer JWT authentication\n    message: API must\
  \ define bearerAuth security scheme\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  remitian-v1-path-prefix:\n    description: All paths must begin with /v1/\n    message: \"Path '{{property}}' must start with /v1/\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  remitian-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{property}}' must use kebab-case segments\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v1/[a-z0-9{}-]+)+(/[a-z0-9{}-]+)*$\"\n\n  remitian-payment-status-enum:\n    description: Payment status fields should use the canonical enum values\n    message: Payment status must be one of the canonical lifecycle values\n    severity: warn\n    given: \"$.components.schemas.*.properties.status.enum\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  remitian-401-on-protected-operations:\n    description: All protected operations must define a 401 response\n    message: Operation must define a 401 Unauthorized response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  remitian-post-request-body-required:\n    description: POST operations must define a requestBody\n    message: POST operations must include a request body schema\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  remitian-pagination-on-list-endpoints:\n    description: List endpoints should support pagination parameters\n    message: Collection GET endpoints should include limit and offset parameters\n    severity: warn\n    given: \"$.paths[?(!/@id)].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          type: object\n\n  remitian-component-refs-used:\n    description: Schemas should use $ref to components where available\n    message: Prefer $ref to shared components over inline schema definitions\n    severity: info\n    given: \"$.paths[*][*].responses[*].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/rules/remitian-rules.yml
tags:
- Tax
- Payments
- Fintech
- Accounting
- Webhooks
- Embedded Payments
- Spectral
- Linting
- API Governance
---
