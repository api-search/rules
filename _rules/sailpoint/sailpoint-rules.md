---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: SailPoint Identity Security Cloud V3 API
  slug: identity-security-cloud-v3-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/v3/identity-security-cloud-v-3-api/
- filename: openapi.yaml
  format: yaml
  label: SailPoint Identity Security Cloud V2024 API
  slug: identity-security-cloud-v2024-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/v2024/identity-security-cloud-v-2024-api/
- filename: openapi.yaml
  format: yaml
  label: SailPoint Identity Security Cloud V2025 API
  slug: identity-security-cloud-v2025-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/v2025/identity-security-cloud-v-2025-api/
- filename: openapi.yaml
  format: yaml
  label: SailPoint Identity Security Cloud Beta API
  slug: identity-security-cloud-beta-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/beta/identity-security-cloud-beta-api/
- filename: openapi.yaml
  format: yaml
  label: SailPoint IdentityIQ SCIM API
  slug: identityiq-scim-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/iiq/identityiq-scim-rest-api/
- filename: openapi.yaml
  format: yaml
  label: SailPoint Identity Security Cloud V2026 API
  slug: identity-security-cloud-v2026-api
  spec_type: OpenAPI
  url: https://developer.sailpoint.com/docs/api/v2026/identity-security-cloud-v-2026-api/
categories:
- sailpoint
description: Spectral linting rules defining API design standards and conventions for SailPoint.
layout: rules
name: SailPoint API Rules
provider_name: SailPoint
provider_slug: sailpoint
rule_count: 10
rules:
- description: OperationIds must use camelCase (SailPoint convention).
  given: $.paths[*][*].operationId
  name: sailpoint-operation-id-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: sailpoint-summary-not-empty
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: sailpoint-tags-required
  severity: warn
- description: All operations must define a 200 or 201 response.
  given: $.paths[*][*].responses
  name: sailpoint-response-200-required
  severity: error
- description: Operations should define standard SailPoint error responses (400, 401, 403, 404, 429, 500).
  given: $.paths[*][*].responses
  name: sailpoint-error-responses-required
  severity: warn
- description: Paths must use kebab-case for multi-word segments.
  given: $.paths[*]~
  name: sailpoint-path-kebab-case
  severity: warn
- description: All operations should declare OAuth2 or PAT security.
  given: $.paths[*][*]
  name: sailpoint-oauth2-security
  severity: warn
- description: List operations should support limit and offset query parameters.
  given: $.paths[*].get
  name: sailpoint-list-operations-pagination
  severity: hint
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: sailpoint-no-trailing-slash
  severity: error
- description: Request bodies should use application/json content type.
  given: $.paths[*][*].requestBody.content
  name: sailpoint-content-type-json
  severity: warn
rules_file: rules/sailpoint-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sailpoint/refs/heads/main/rules/sailpoint-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: sailpoint-rules
source_filename: sailpoint-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # SailPoint API naming conventions\n  sailpoint-operation-id-camel-case:\n    description: OperationIds must use camelCase (SailPoint convention).\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sailpoint-summary-not-empty:\n    description: All operations must have a summary.\n    message: \"Operation must have a non-empty summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  sailpoint-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  sailpoint-response-200-required:\n    description: All operations must define\
  \ a 200 or 201 response.\n    message: \"Operation must define a success response (200 or 201).\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  sailpoint-error-responses-required:\n    description: Operations should define standard SailPoint error responses (400, 401, 403, 404, 429, 500).\n    message: \"Operation should define standard error responses.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"400\", \"401\", \"403\"]\n\n  sailpoint-path-kebab-case:\n    description: Paths must use kebab-case for multi-word segments.\n    message: \"Path segment '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^(/[a-z0-9{}-]+-?[a-z0-9{}-]*)*$\"\n\n  sailpoint-oauth2-security:\n    description: All operations should declare OAuth2 or PAT security.\n    message: \"Operation must declare security (oauth2 or personalAccessToken).\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  sailpoint-list-operations-pagination:\n    description: List operations should support limit and offset query parameters.\n    message: \"List operation should support pagination parameters (limit, offset).\"\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n              contains:\n                type: object\n                properties:\n                  name:\n                    enum: [limit, offset]\n\n  sailpoint-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n\
  \    message: \"Path '{{value}}' must not end with a slash.\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  sailpoint-content-type-json:\n    description: Request bodies should use application/json content type.\n    message: \"Request body must specify application/json content type.\"\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"application/json\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sailpoint/refs/heads/main/rules/sailpoint-rules.yml
tags:
- Access Governance
- Compliance
- IAM
- Identity Management
- Identity Security
- Security
- Spectral
- Linting
- API Governance
---
