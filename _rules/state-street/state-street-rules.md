---
api_specs:
- filename: state-street-alpha-data-platform-openapi.yml
  format: yaml
  label: Alpha Data Platform API
  slug: alpha-data-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/state-street/refs/heads/main/openapi/state-street-alpha-data-platform-openapi.yml
- filename: state-street-fund-connect-openapi.yml
  format: yaml
  label: Fund Connect API
  slug: fund-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/state-street/refs/heads/main/openapi/state-street-fund-connect-openapi.yml
categories:
- state
description: Spectral linting rules defining API design standards and conventions for State Street.
layout: rules
name: State Street API Rules
provider_name: State Street
provider_slug: state-street
rule_count: 16
rules:
- description: All State Street APIs must include contact information
  given: $.info
  name: state-street-info-contact-required
  severity: error
- description: Operation summaries must use Title Case per State Street API standards
  given: $.paths[*][get,post,put,patch,delete].summary
  name: state-street-operation-summary-title-case
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: state-street-operation-id-camel-case
  severity: error
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: state-street-operation-tags-required
  severity: error
- description: All paths must start with a version prefix
  given: $.paths
  name: state-street-path-versioned
  severity: error
- description: State Street APIs must use OAuth2 Client Credentials
  given: $.components.securitySchemes[*]
  name: state-street-oauth2-required
  severity: error
- description: OAuth2 must use Client Credentials flow per RFC 6749 Section 4.4.2
  given: $.components.securitySchemes[*][?(@.type=='oauth2')].flows
  name: state-street-oauth2-client-credentials
  severity: error
- description: APIs should support X-Correlation-ID header for request tracing
  given: $.components.parameters
  name: state-street-correlation-id-header
  severity: warn
- description: List operations must support pagination
  given: $.paths[*].get.parameters
  name: state-street-pagination-get-lists
  severity: warn
- description: APIs must document rate limiting responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: state-street-response-429-rate-limit
  severity: warn
- description: API must use application/json as the primary content type
  given: $.paths[*][get,post,put,patch,delete].responses['200'].content
  name: state-street-json-default-format
  severity: error
- description: All schema components must have descriptions
  given: $.components.schemas[*]
  name: state-street-schema-description
  severity: warn
- description: Error responses should reference the standard Error schema
  given: $.paths[*][get,post,put,patch,delete].responses[4*,5*].content['application/json']
  name: state-street-error-schema-consistent
  severity: warn
- description: API must apply security globally
  given: $
  name: state-street-security-global
  severity: error
- description: API must define servers
  given: $
  name: state-street-servers-defined
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: state-street-parameter-description
  severity: warn
rules_file: rules/state-street-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/state-street/refs/heads/main/rules/state-street-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 0
  warn: 6
slug: state-street-rules
source_filename: state-street-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  state-street-info-contact-required:\n    description: All State Street APIs must include contact information\n    message: API info must include contact email and URL\n    severity: error\n    given: $.info\n    then:\n      - field: contact.email\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  state-street-operation-summary-title-case:\n    description: Operation summaries must use Title Case per State Street API standards\n    message: Operation summary must use Title Case\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(?: [A-Z][a-zA-Z0-9]*)*$'\n\n  state-street-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: OperationId must be camelCase\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  state-street-operation-tags-required:\n    description: All operations must be tagged\n    message: Operation must include at least one tag\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  state-street-path-versioned:\n    description: All paths must start with a version prefix\n    message: Paths must begin with /v1/ or similar version prefix\n    severity: error\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^/v[0-9]+/'\n\n  state-street-oauth2-required:\n    description: State Street APIs must use OAuth2 Client Credentials\n    message: API must define OAuth2 security scheme\n    severity: error\n    given: $.components.securitySchemes[*]\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: '^oauth2$'\n\
  \n  state-street-oauth2-client-credentials:\n    description: OAuth2 must use Client Credentials flow per RFC 6749 Section 4.4.2\n    message: OAuth2 scheme must include clientCredentials flow\n    severity: error\n    given: $.components.securitySchemes[*][?(@.type=='oauth2')].flows\n    then:\n      field: clientCredentials\n      function: truthy\n\n  state-street-correlation-id-header:\n    description: APIs should support X-Correlation-ID header for request tracing\n    message: API should define X-Correlation-ID parameter for tracing\n    severity: warn\n    given: $.components.parameters\n    then:\n      field: XCorrelationId\n      function: truthy\n\n  state-street-pagination-get-lists:\n    description: List operations must support pagination\n    message: GET list operations should support pageSize and pageToken parameters\n    severity: warn\n    given: $.paths[*].get.parameters\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\
  \          contains:\n            type: object\n            properties:\n              name:\n                enum:\n                  - pageSize\n                  - pageToken\n\n  state-street-response-429-rate-limit:\n    description: APIs must document rate limiting responses\n    message: Operations should define 429 Too Many Requests with Retry-After header\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required:\n                - '429'\n            - required:\n                - '200'\n\n  state-street-json-default-format:\n    description: API must use application/json as the primary content type\n    message: Operations must support application/json content type\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses['200'].content\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          required:\n            - application/json\n\n  state-street-schema-description:\n    description: All schema components must have descriptions\n    message: Schema component must include a description\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  state-street-error-schema-consistent:\n    description: Error responses should reference the standard Error schema\n    message: Error responses should reference the reusable Error schema component\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[4*,5*].content['application/json']\n    then:\n      field: schema\n      function: truthy\n\n  state-street-security-global:\n    description: API must apply security globally\n    message: API must define global security requirement\n    severity: error\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  state-street-servers-defined:\n\
  \    description: API must define servers\n    message: API must specify at least one server URL\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  state-street-parameter-description:\n    description: All parameters must have descriptions\n    message: Parameter must include a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/state-street/refs/heads/main/rules/state-street-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
