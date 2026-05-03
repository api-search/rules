---
api_specs:
- filename: veracode-applications-openapi.yml
  format: yaml
  label: Veracode Applications REST API
  slug: veracode-applications-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/openapi/veracode-applications-openapi.yml
- filename: veracode-findings-openapi.yml
  format: yaml
  label: Veracode Findings REST API
  slug: veracode-findings-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/openapi/veracode-findings-openapi.yml
- filename: veracode-identity-openapi.yml
  format: yaml
  label: Veracode Identity REST API
  slug: veracode-identity-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/openapi/veracode-identity-openapi.yml
- filename: veracode-reporting-openapi.yml
  format: yaml
  label: Veracode Reporting REST API
  slug: veracode-reporting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/openapi/veracode-reporting-openapi.yml
categories:
- veracode
description: Spectral linting rules defining API design standards and conventions for Veracode.
layout: rules
name: Veracode API Rules
provider_name: Veracode
provider_slug: veracode
rule_count: 11
rules:
- description: Veracode APIs must define HMAC security scheme
  given: $.components.securitySchemes[*]
  name: veracode-hmac-auth-defined
  severity: error
- description: Veracode API paths must use /appsec/ or /api/authn/ prefix
  given: $.paths[*]~
  name: veracode-path-prefix
  severity: error
- description: All operations must define an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: veracode-operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: veracode-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: veracode-summary-title-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: veracode-summary-required
  severity: error
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: veracode-401-response
  severity: error
- description: Properties named 'guid' should use uuid format
  given: $.components.schemas[*].properties.guid
  name: veracode-guid-uuid-format
  severity: warn
- description: Collection responses should use HAL _embedded structure
  given: $.components.schemas[*]
  name: veracode-hal-embedded-pattern
  severity: hint
- description: API paths should include version (v1, v2, etc.)
  given: $.paths[*]~
  name: veracode-api-version-in-path
  severity: warn
- description: API info must include contact information
  given: $.info
  name: veracode-info-contact
  severity: warn
rules_file: rules/veracode-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/rules/veracode-rules.yml
severity_counts:
  error: 5
  hint: 1
  info: 0
  warn: 5
slug: veracode-rules
source_filename: veracode-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Veracode APIs use HMAC authentication\n  veracode-hmac-auth-defined:\n    description: Veracode APIs must define HMAC security scheme\n    message: Security scheme must use veracode_hmac scheme\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: \"veracode_hmac\"\n\n  # All paths must use /appsec/ or /api/authn/ prefix\n  veracode-path-prefix:\n    description: Veracode API paths must use /appsec/ or /api/authn/ prefix\n    message: \"Path '{{value}}' must start with /appsec/ or /api/authn/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/appsec/|/api/authn/)\"\n\n  # All operations must have operationId\n  veracode-operation-id-required:\n    description: All operations must define an operationId\n    message: Operation must have an operationId\n\
  \    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId should be camelCase\n  veracode-operation-id-camel-case:\n    description: operationId should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries must be Title Case\n  veracode-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # All operations need summaries\n  veracode-summary-required:\n    description: All operations must\
  \ have a summary\n    message: Operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Must define 401 response (HMAC auth is always required)\n  veracode-401-response:\n    description: All operations must document 401 Unauthorized response\n    message: Operation must define a 401 response for HMAC authentication failures\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # GUIDs should be uuid format\n  veracode-guid-uuid-format:\n    description: Properties named 'guid' should use uuid format\n    message: GUID property should have format uuid\n    severity: warn\n    given: \"$.components.schemas[*].properties.guid\"\n    then:\n      field: format\n      function: truthy\n\n  # Response schemas should use HAL _embedded pattern\n  veracode-hal-embedded-pattern:\n    description:\
  \ Collection responses should use HAL _embedded structure\n    message: List responses should use _embedded container pattern\n    severity: hint\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # API version in path\n  veracode-api-version-in-path:\n    description: API paths should include version (v1, v2, etc.)\n    message: \"Path '{{value}}' should include API version\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]/\"\n\n  # Contact info required\n  veracode-info-contact:\n    description: API info must include contact information\n    message: API info must include contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/veracode/refs/heads/main/rules/veracode-rules.yml
tags:
- Application Security
- SAST
- DAST
- SCA
- Security Testing
- DevSecOps
- Spectral
- Linting
- API Governance
---
