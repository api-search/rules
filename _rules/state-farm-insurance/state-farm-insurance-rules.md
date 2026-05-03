---
api_specs:
- filename: state-farm-insurance-renters-openapi.yml
  format: yaml
  label: Renters Insurance API
  slug: renters-insurance-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/state-farm-insurance/refs/heads/main/openapi/state-farm-insurance-renters-openapi.yml
categories:
- state
description: Spectral linting rules defining API design standards and conventions for State Farm Insurance.
layout: rules
name: State Farm Insurance API Rules
provider_name: State Farm Insurance
provider_slug: state-farm-insurance
rule_count: 15
rules:
- description: All State Farm Insurance APIs must include contact information
  given: $.info
  name: state-farm-insurance-info-contact-required
  severity: error
- description: Operation summaries must use Title Case per State Farm Insurance API conventions
  given: $.paths[*][get,post,put,patch,delete].summary
  name: state-farm-insurance-operation-summary-title-case
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: state-farm-insurance-operation-id-camel-case
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: state-farm-insurance-operation-tags-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: state-farm-insurance-operation-description-required
  severity: warn
- description: All API paths must start with a version prefix /v1
  given: $.paths
  name: state-farm-insurance-path-versioned
  severity: error
- description: Path segments must use kebab-case
  given: $.paths
  name: state-farm-insurance-path-kebab-case
  severity: error
- description: All insurance APIs must use OAuth2 authentication
  given: $.components.securitySchemes[*]
  name: state-farm-insurance-oauth2-security
  severity: error
- description: Global security must be applied at the API level
  given: $
  name: state-farm-insurance-security-applied
  severity: error
- description: POST operations that create resources must return 201
  given: $.paths[*].post.responses
  name: state-farm-insurance-response-201-post
  severity: warn
- description: Operations must define error response codes
  given: $.paths[*][get,post,put,patch,delete].responses
  name: state-farm-insurance-response-error-codes
  severity: warn
- description: All schema components must have descriptions
  given: $.components.schemas[*]
  name: state-farm-insurance-schema-description
  severity: warn
- description: All parameters must explicitly declare whether they are required
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: state-farm-insurance-parameter-required-flag
  severity: warn
- description: State code fields should validate US state abbreviations
  given: $.components.schemas[*].properties.state
  name: state-farm-insurance-state-code-pattern
  severity: info
- description: Request bodies must use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: state-farm-insurance-request-body-content-type
  severity: error
rules_file: rules/state-farm-insurance-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/state-farm-insurance/refs/heads/main/rules/state-farm-insurance-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 1
  warn: 5
slug: state-farm-insurance-rules
source_filename: state-farm-insurance-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  state-farm-insurance-info-contact-required:\n    description: All State Farm Insurance APIs must include contact information\n    message: API info object must include contact with URL pointing to developer portal\n    severity: error\n    given: $.info\n    then:\n      - field: contact\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  state-farm-insurance-operation-summary-title-case:\n    description: Operation summaries must use Title Case per State Farm Insurance API conventions\n    message: Operation summary must use Title Case\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(?: [A-Z][a-zA-Z0-9]*)*$'\n\n  state-farm-insurance-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: OperationId must be camelCase\n    severity: error\n \
  \   given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  state-farm-insurance-operation-tags-required:\n    description: All operations must have tags\n    message: Operation must include at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  state-farm-insurance-operation-description-required:\n    description: All operations must have a description\n    message: Operation must include a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  state-farm-insurance-path-versioned:\n    description: All API paths must start with a version prefix /v1\n    message: Paths must begin with /v1/ version prefix\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n\
  \      functionOptions:\n        match: '^/v[0-9]+/'\n\n  state-farm-insurance-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: Path segments must use kebab-case (lowercase, hyphens)\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^(/v[0-9]+)(/[a-z][a-z0-9-]*|/{[a-zA-Z][a-zA-Z0-9]*})*/?$'\n\n  state-farm-insurance-oauth2-security:\n    description: All insurance APIs must use OAuth2 authentication\n    message: API must define OAuth2 security scheme\n    severity: error\n    given: $.components.securitySchemes[*]\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: '^oauth2$'\n\n  state-farm-insurance-security-applied:\n    description: Global security must be applied at the API level\n    message: API must apply security globally or per operation\n    severity: error\n    given: $\n    then:\n      field: security\n    \
  \  function: truthy\n\n  state-farm-insurance-response-201-post:\n    description: POST operations that create resources must return 201\n    message: POST operations creating resources should return 201 Created\n    severity: warn\n    given: $.paths[*].post.responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required:\n                - '201'\n            - required:\n                - '200'\n\n  state-farm-insurance-response-error-codes:\n    description: Operations must define error response codes\n    message: Operations should define 400, 401, and appropriate error codes\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required:\n                - '400'\n            - required:\n                - '401'\n            - required:\n\
  \                - '404'\n\n  state-farm-insurance-schema-description:\n    description: All schema components must have descriptions\n    message: Schema component must include a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  state-farm-insurance-parameter-required-flag:\n    description: All parameters must explicitly declare whether they are required\n    message: Parameter must include explicit required field\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: required\n      function: defined\n\n  state-farm-insurance-state-code-pattern:\n    description: State code fields should validate US state abbreviations\n    message: State fields should use a 2-letter uppercase pattern\n    severity: info\n    given: $.components.schemas[*].properties.state\n    then:\n      field: pattern\n      function: truthy\n\n  state-farm-insurance-request-body-content-type:\n\
  \    description: Request bodies must use application/json content type\n    message: Request body must specify application/json content type\n    severity: error\n    given: $.paths[*][post,put,patch].requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - application/json\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/state-farm-insurance/refs/heads/main/rules/state-farm-insurance-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
