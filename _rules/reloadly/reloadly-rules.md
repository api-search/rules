---
api_specs:
- filename: reloadly-gift-cards-openapi.yml
  format: yaml
  label: Reloadly Gift Cards API
  slug: gift-cards
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reloadly/refs/heads/main/openapi/reloadly-gift-cards-openapi.yml
- filename: reloadly-airtime-openapi.yml
  format: yaml
  label: Reloadly Airtime API
  slug: airtime
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reloadly/refs/heads/main/openapi/reloadly-airtime-openapi.yml
categories:
- reloadly
description: Spectral linting rules defining API design standards and conventions for Reloadly.
layout: rules
name: Reloadly API Rules
provider_name: Reloadly
provider_slug: reloadly
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: reloadly-operation-ids-camel-case
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: reloadly-summary-title-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: reloadly-tags-required
  severity: error
- description: API must define bearerAuth security scheme
  given: $.components.securitySchemes
  name: reloadly-bearer-auth-required
  severity: error
- description: Collection endpoints must support page and size parameters
  given: $.paths[*].get
  name: reloadly-pagination-parameters
  severity: warn
- description: Operations must define 401 error responses
  given: $.paths[?(!/@oauth)][*]
  name: reloadly-error-response-defined
  severity: error
- description: Successful responses must have a schema
  given: $.paths[*][*].responses[200,201].content.application/json
  name: reloadly-response-200-schema
  severity: warn
- description: POST/PUT request bodies must have schemas
  given: $.paths[*][post,put].requestBody.content.application/json
  name: reloadly-request-body-schema
  severity: error
- description: Token request must include audience parameter
  given: $.paths['/oauth/token'].post.requestBody.content.application/json.schema.required
  name: reloadly-audience-parameter
  severity: error
- description: Path segments must use kebab-case
  given: $.paths
  name: reloadly-path-kebab-case
  severity: warn
rules_file: rules/reloadly-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reloadly/refs/heads/main/rules/reloadly-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 4
slug: reloadly-rules
source_filename: reloadly-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  reloadly-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  reloadly-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 -]*$\"\n\n  reloadly-tags-required:\n    description: Every operation must have at least one tag\n    message: Operation must include at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  reloadly-bearer-auth-required:\n    description: API must define bearerAuth security scheme\n    message:\
  \ API must use Bearer token authentication\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  reloadly-pagination-parameters:\n    description: Collection endpoints must support page and size parameters\n    message: GET collection endpoints should include page and size query parameters\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  reloadly-error-response-defined:\n    description: Operations must define 401 error responses\n    message: Operation must define a 401 Unauthorized response\n    severity: error\n    given: \"$.paths[?(!/@oauth)][*]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '401'\n\n  reloadly-response-200-schema:\n    description: Successful responses must have a schema\n\
  \    message: 200/201 response must include a content schema\n    severity: warn\n    given: \"$.paths[*][*].responses[200,201].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  reloadly-request-body-schema:\n    description: POST/PUT request bodies must have schemas\n    message: POST/PUT operations must define a requestBody schema\n    severity: error\n    given: \"$.paths[*][post,put].requestBody.content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  reloadly-audience-parameter:\n    description: Token request must include audience parameter\n    message: OAuth token request must include the audience parameter\n    severity: error\n    given: \"$.paths['/oauth/token'].post.requestBody.content.application/json.schema.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: audience\n\n  reloadly-path-kebab-case:\n    description:\
  \ Path segments must use kebab-case\n    message: \"Path segment '{{value}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reloadly/refs/heads/main/rules/reloadly-rules.yml
tags:
- Gift Cards
- Payments
- Airtime
- Mobile Top-Up
- Rewards
- Incentives
- Spectral
- Linting
- API Governance
---
