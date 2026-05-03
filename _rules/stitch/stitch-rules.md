---
api_specs:
- filename: stitch-openapi.yml
  format: yaml
  label: Stitch GraphQL API
  slug: stitch-graphql
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stitch/refs/heads/main/openapi/stitch-openapi.yml
categories:
- stitch
description: Spectral linting rules defining API design standards and conventions for Stitch.
layout: rules
name: Stitch API Rules
provider_name: Stitch
provider_slug: stitch
rule_count: 7
rules:
- description: All Stitch GraphQL operations must use Bearer token authentication obtained from the OAuth 2.0 token endpoint.
  given: $.components.securitySchemes
  name: stitch-bearer-auth-required
  severity: error
- description: The Stitch GraphQL endpoint (/graphql) must only accept POST requests.
  given: $.paths./graphql
  name: stitch-graphql-endpoint-post-only
  severity: error
- description: All Stitch operations must define a 200 success response.
  given: $.paths[*][*]
  name: stitch-response-200-required
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: stitch-operationid-camel-case
  severity: warn
- description: All operation tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: stitch-tags-title-case
  severity: warn
- description: All Stitch API servers must use HTTPS.
  given: $.servers[*].url
  name: stitch-server-https
  severity: error
- description: The Stitch OAuth token endpoint must accept application/x-www-form-urlencoded content type per OAuth 2.0 specification.
  given: $.paths./connect/token.post.requestBody.content
  name: stitch-token-endpoint-form-encoded
  severity: error
rules_file: rules/stitch-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stitch/refs/heads/main/rules/stitch-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 2
slug: stitch-rules
source_filename: stitch-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stitch-bearer-auth-required:\n    description: >-\n      All Stitch GraphQL operations must use Bearer token authentication\n      obtained from the OAuth 2.0 token endpoint.\n    message: \"Operations must declare BearerAuth security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: defined\n\n  stitch-graphql-endpoint-post-only:\n    description: >-\n      The Stitch GraphQL endpoint (/graphql) must only accept POST requests.\n    message: \"GraphQL endpoint must use POST method.\"\n    severity: error\n    given: \"$.paths./graphql\"\n    then:\n      field: post\n      function: defined\n\n  stitch-response-200-required:\n    description: All Stitch operations must define a 200 success response.\n    message: \"Operation '{{operationId}}' is missing a 200 response.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.200\n  \
  \    function: defined\n\n  stitch-operationid-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stitch-tags-title-case:\n    description: All operation tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  stitch-server-https:\n    description: All Stitch API servers must use HTTPS.\n    message: \"Server URL must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  stitch-token-endpoint-form-encoded:\n    description: >-\n      The Stitch OAuth token\
  \ endpoint must accept application/x-www-form-urlencoded\n      content type per OAuth 2.0 specification.\n    message: \"Token endpoint must accept application/x-www-form-urlencoded.\"\n    severity: error\n    given: \"$.paths./connect/token.post.requestBody.content\"\n    then:\n      field: application/x-www-form-urlencoded\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stitch/refs/heads/main/rules/stitch-rules.yml
tags:
- Africa
- Financial Data
- Open Banking
- Payments
- Unified API
- South Africa
- Nigeria
- Spectral
- Linting
- API Governance
---
