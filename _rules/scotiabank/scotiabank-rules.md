---
api_specs:
- filename: scotiabank-tranxact-openapi.yml
  format: yaml
  label: Scotia TranXact APIs
  slug: scotia-tranxact
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scotiabank/refs/heads/main/openapi/scotiabank-tranxact-openapi.yml
categories:
- scotiabank
description: Spectral linting rules defining API design standards and conventions for Scotiabank.
layout: rules
name: Scotiabank API Rules
provider_name: Scotiabank
provider_slug: scotiabank
rule_count: 10
rules:
- description: All operations must use OAuth2 authentication
  given: $.components.securitySchemes
  name: scotiabank-oauth2-security
  severity: error
- description: All operations must have operationId
  given: $.paths[*][*]
  name: scotiabank-operation-ids
  severity: error
- description: API paths must include version prefix
  given: $.paths
  name: scotiabank-versioned-paths
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: scotiabank-tags-required
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: scotiabank-camel-case-operation-ids
  severity: warn
- description: Payment request bodies must include amount field
  given: $.paths[?(@property.match(/payments/))].post.requestBody.content.application/json.schema
  name: scotiabank-payment-amount-required
  severity: error
- description: Operations should document standard error responses
  given: $.paths[*][*].responses
  name: scotiabank-error-responses
  severity: warn
- description: Account path parameters should be clearly named
  given: $.paths[*][*].parameters[?(@.in === 'path')]
  name: scotiabank-account-id-path-params
  severity: warn
- description: Currency fields should be constrained to supported currencies
  given: $.components.schemas[*].properties.currency
  name: scotiabank-currency-enum
  severity: info
- description: Date fields should use ISO 8601 format
  given: $.components.schemas[*].properties[?(@ =~ /date|time/i)]
  name: scotiabank-date-format
  severity: warn
rules_file: rules/scotiabank-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scotiabank/refs/heads/main/rules/scotiabank-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: scotiabank-rules
source_filename: scotiabank-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  scotiabank-oauth2-security:\n    description: All operations must use OAuth2 authentication\n    message: \"Scotiabank APIs require OAuth2 client credentials authentication\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: OAuth2\n      function: truthy\n\n  scotiabank-operation-ids:\n    description: All operations must have operationId\n    message: \"Every operation must have a unique operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  scotiabank-versioned-paths:\n    description: API paths must include version prefix\n    message: \"API paths must start with /v1/ for versioning\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  scotiabank-tags-required:\n    description: All operations must have at least one tag\n    message:\
  \ \"Operations must be tagged for proper categorization\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  scotiabank-camel-case-operation-ids:\n    description: Operation IDs should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase naming\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  scotiabank-payment-amount-required:\n    description: Payment request bodies must include amount field\n    message: \"Payment operations should require an 'amount' field in the request body\"\n    severity: error\n    given: \"$.paths[?(@property.match(/payments/))].post.requestBody.content.application/json.schema\"\n    then:\n      field: required\n      function: truthy\n\n  scotiabank-error-responses:\n    description: Operations should document standard error responses\n    message: \"Operations\
  \ should document 400, 401, and 422 error responses\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '401'\n\n  scotiabank-account-id-path-params:\n    description: Account path parameters should be clearly named\n    message: \"Account path parameters should use descriptive names like 'account_id'\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in === 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z_]*_?(id|number)$|^id$\"\n\n  scotiabank-currency-enum:\n    description: Currency fields should be constrained to supported currencies\n    message: \"Currency fields should use enum to restrict to supported values (CAD, USD)\"\n    severity: info\n    given: \"$.components.schemas[*].properties.currency\"\n    then:\n      field: enum\n      function: truthy\n\
  \n  scotiabank-date-format:\n    description: Date fields should use ISO 8601 format\n    message: \"Date fields should use 'date' or 'date-time' format\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@ =~ /date|time/i)]\"\n    then:\n      field: format\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scotiabank/refs/heads/main/rules/scotiabank-rules.yml
tags:
- Banking
- Finance
- Payments
- Canada
- Open Banking
- Spectral
- Linting
- API Governance
---
