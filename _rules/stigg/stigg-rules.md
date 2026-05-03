---
api_specs:
- filename: stigg-openapi.yml
  format: yaml
  label: Stigg GraphQL API
  slug: stigg-graphql
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stigg/refs/heads/main/openapi/stigg-openapi.yml
categories:
- stigg
description: Spectral linting rules defining API design standards and conventions for Stigg.
layout: rules
name: Stigg API Rules
provider_name: Stigg
provider_slug: stigg
rule_count: 7
rules:
- description: All Stigg API operations must require the X-API-KEY header for authentication.
  given: $.components.securitySchemes
  name: stigg-x-api-key-required
  severity: error
- description: The Stigg GraphQL endpoint (/graphql) must only accept POST requests, following GraphQL convention.
  given: $.paths./graphql
  name: stigg-graphql-endpoint-post-only
  severity: error
- description: All POST operations to the GraphQL endpoint must define a request body.
  given: $.paths./graphql.post
  name: stigg-request-body-required-for-graphql
  severity: error
- description: All Stigg operations must define a 200 success response.
  given: $.paths[*][*]
  name: stigg-response-200-required
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: stigg-operationid-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: stigg-tags-title-case
  severity: warn
- description: The Stigg API server must use HTTPS.
  given: $.servers[*].url
  name: stigg-server-https
  severity: error
rules_file: rules/stigg-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stigg/refs/heads/main/rules/stigg-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 2
slug: stigg-rules
source_filename: stigg-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stigg-x-api-key-required:\n    description: >-\n      All Stigg API operations must require the X-API-KEY header for\n      authentication.\n    message: \"Operations must declare X-API-KEY security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: ApiKey\n      function: defined\n\n  stigg-graphql-endpoint-post-only:\n    description: >-\n      The Stigg GraphQL endpoint (/graphql) must only accept POST requests,\n      following GraphQL convention.\n    message: \"GraphQL endpoint must use POST method.\"\n    severity: error\n    given: \"$.paths./graphql\"\n    then:\n      field: post\n      function: defined\n\n  stigg-request-body-required-for-graphql:\n    description: All POST operations to the GraphQL endpoint must define a request body.\n    message: \"GraphQL POST operation must define a requestBody.\"\n    severity: error\n    given: \"$.paths./graphql.post\"\n    then:\n      field:\
  \ requestBody\n      function: defined\n\n  stigg-response-200-required:\n    description: All Stigg operations must define a 200 success response.\n    message: \"Operation '{{operationId}}' is missing a 200 response.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.200\n      function: defined\n\n  stigg-operationid-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stigg-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  stigg-server-https:\n    description: The Stigg API server\
  \ must use HTTPS.\n    message: \"Server URL must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stigg/refs/heads/main/rules/stigg-rules.yml
tags:
- FinOps
- Pricing
- Billing
- Entitlements
- Usage-Based Billing
- SaaS
- Spectral
- Linting
- API Governance
---
