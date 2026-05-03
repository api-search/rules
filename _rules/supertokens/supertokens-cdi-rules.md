---
api_specs:
- filename: supertokens-core-driver-interface-openapi.yml
  format: yaml
  label: SuperTokens Core Driver Interface
  slug: core-driver-interface
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supertokens/refs/heads/main/openapi/supertokens-core-driver-interface-openapi.yml
categories:
- supertokens
description: Spectral linting rules defining API design standards and conventions for SuperTokens.
layout: rules
name: SuperTokens API Rules
provider_name: SuperTokens
provider_slug: supertokens
rule_count: 10
rules:
- description: All SuperTokens CDI operations must have an operationId
  given: $.paths[*][*]
  name: supertokens-operation-id-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: supertokens-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: supertokens-tags-required
  severity: warn
- description: All 200 response bodies should contain a status field for error handling
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: supertokens-status-in-response
  severity: warn
- description: CDI API must define api-key security scheme
  given: $.components.securitySchemes
  name: supertokens-api-key-security
  severity: error
- description: POST operations must have a request body
  given: $.paths[*].post
  name: supertokens-request-body-for-post
  severity: error
- description: PUT operations must have a request body
  given: $.paths[*].put
  name: supertokens-request-body-for-put
  severity: error
- description: tenantId parameters should have a description
  given: $.paths[*][*].parameters[?(@.name == 'tenantId')]
  name: supertokens-tenant-id-described
  severity: warn
- description: User schema must include id and timeJoined fields
  given: $.components.schemas.User.properties
  name: supertokens-user-schema-required
  severity: error
- description: 401 error responses should be defined for session endpoints
  given: $.paths['/recipe/session'].get.responses
  name: supertokens-error-response-defined
  severity: warn
rules_file: rules/supertokens-cdi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/supertokens/refs/heads/main/rules/supertokens-cdi-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: supertokens-cdi-rules
source_filename: supertokens-cdi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  supertokens-operation-id-required:\n    description: All SuperTokens CDI operations must have an operationId\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: truthy\n\n  supertokens-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: $.paths[*][*].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*([ \\/][A-Z][a-zA-Z0-9]*)*$'\n\n  supertokens-tags-required:\n    description: All operations must have at least one tag\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: truthy\n\n  supertokens-status-in-response:\n    description: All 200 response bodies should contain a status field for error handling\n    severity: warn\n    given: $.paths[*][*].responses.200.content.application/json.schema.properties\n    then:\n      field: status\n      function: truthy\n\n  supertokens-api-key-security:\n\
  \    description: CDI API must define api-key security scheme\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - ApiKeyAuth\n\n  supertokens-request-body-for-post:\n    description: POST operations must have a request body\n    severity: error\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  supertokens-request-body-for-put:\n    description: PUT operations must have a request body\n    severity: error\n    given: $.paths[*].put\n    then:\n      field: requestBody\n      function: truthy\n\n  supertokens-tenant-id-described:\n    description: tenantId parameters should have a description\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.name == 'tenantId')]\n    then:\n      field: description\n      function: truthy\n\n  supertokens-user-schema-required:\n    description: User schema must include id and timeJoined\
  \ fields\n    severity: error\n    given: $.components.schemas.User.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - id\n            - timeJoined\n\n  supertokens-error-response-defined:\n    description: 401 error responses should be defined for session endpoints\n    severity: warn\n    given: $.paths['/recipe/session'].get.responses\n    then:\n      field: '401'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/supertokens/refs/heads/main/rules/supertokens-cdi-rules.yml
tags:
- Authentication
- Open Source
- Session Management
- Social Login
- Passwordless
- Identity
- Authorization
- Multi-Tenancy
- Node.js
- Self-Hosted
- Spectral
- Linting
- API Governance
---
