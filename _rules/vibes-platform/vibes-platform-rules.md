---
api_specs:
- filename: vibes-platform-openapi.yml
  format: yaml
  label: Vibes Platform API
  slug: vibes-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/openapi/vibes-platform-openapi.yml
- filename: vibes-connect-openapi.yml
  format: yaml
  label: Vibes Connect API
  slug: vibes-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/openapi/vibes-connect-openapi.yml
categories:
- vibes
description: Spectral linting rules defining API design standards and conventions for Vibes Platform.
layout: rules
name: Vibes Platform API Rules
provider_name: Vibes Platform
provider_slug: vibes-platform
rule_count: 13
rules:
- description: All Vibes Platform API paths must include the company_key path parameter.
  given: $.paths[*]
  name: vibes-company-key-path-required
  severity: warn
- description: Operation IDs must use camelCase naming.
  given: $.paths[*][*].operationId
  name: vibes-operationid-camel-case
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: vibes-operation-summary-title-case
  severity: warn
- description: Every operation must have a 200 or 201 success response.
  given: $.paths[*][get,post,put,patch]
  name: vibes-response-200-or-201-required
  severity: error
- description: All operations must include a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: vibes-401-response-required
  severity: warn
- description: All operations must include a 429 Too Many Requests response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: vibes-429-response-required
  severity: warn
- description: Vibes Platform APIs use HTTP Basic authentication.
  given: $.components.securitySchemes
  name: vibes-basic-auth-security
  severity: error
- description: POST and PUT request bodies must use application/json content type.
  given: $.paths[*][post,put].requestBody.content
  name: vibes-request-body-json
  severity: warn
- description: Success responses must return application/json content.
  given: $.paths[*][*].responses[200,201].content
  name: vibes-response-json-content
  severity: warn
- description: API paths must not have trailing slashes.
  given: $.paths[*]~
  name: vibes-no-trailing-slash
  severity: warn
- description: Path segments must use lowercase kebab-case.
  given: $.paths[*]~
  name: vibes-path-kebab-case
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: vibes-operation-description-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete].tags
  name: vibes-tag-required
  severity: warn
rules_file: rules/vibes-platform-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/rules/vibes-platform-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 11
slug: vibes-platform-rules
source_filename: vibes-platform-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Vibes Platform API conventions\n  vibes-company-key-path-required:\n    description: All Vibes Platform API paths must include the company_key path parameter.\n    message: \"Path '{{path}}' should include {company_key} as the first path segment pattern.\"\n    severity: warn\n    given: \"$.paths[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/companies/\\\\{company_key\\\\}\"\n\n  vibes-operationid-camel-case:\n    description: Operation IDs must use camelCase naming.\n    message: \"Operation ID '{{value}}' must be in camelCase format.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vibes-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  vibes-response-200-or-201-required:\n    description: Every operation must have a 200 or 201 success response.\n    message: \"Operation at '{{path}}' must define a 200 or 201 response.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n              anyOf:\n                - required: ['200']\n                - required: ['201']\n\n  vibes-401-response-required:\n    description: All operations must include a 401 Unauthorized response.\n    message: \"Operation at '{{path}}' must define a 401 response for authentication failures.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          required: ['401']\n\n  vibes-429-response-required:\n    description: All operations must include a 429 Too Many Requests response.\n    message: \"Operation at '{{path}}' must define a 429 response for rate limiting.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['429']\n\n  vibes-basic-auth-security:\n    description: Vibes Platform APIs use HTTP Basic authentication.\n    message: \"API must define basicAuth as a security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['basicAuth']\n\n  vibes-request-body-json:\n    description: POST and PUT request bodies must use application/json content type.\n    message: \"Request body for\
  \ '{{path}}' must use application/json.\"\n    severity: warn\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['application/json']\n\n  vibes-response-json-content:\n    description: Success responses must return application/json content.\n    message: \"Response must use application/json content type.\"\n    severity: warn\n    given: \"$.paths[*][*].responses[200,201].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['application/json']\n\n  vibes-no-trailing-slash:\n    description: API paths must not have trailing slashes.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*/$\"\n\n  vibes-path-kebab-case:\n    description: Path\
  \ segments must use lowercase kebab-case.\n    message: \"Path '{{value}}' should use lowercase kebab-case segments.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  vibes-operation-description-required:\n    description: All operations must have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  vibes-tag-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/rules/vibes-platform-rules.yml
tags:
- Mobile Marketing
- Mobile Messaging
- Push Notifications
- SMS
- MMS
- Broadcast Messaging
- Acquisition Campaigns
- Subscription Management
- Wallet Passes
- RCS
- Spectral
- Linting
- API Governance
---
