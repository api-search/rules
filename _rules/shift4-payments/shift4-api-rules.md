---
api_specs:
- filename: shift4-api-openapi.yml
  format: yaml
  label: Shift4 Payments API
  slug: shift4-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shift4-payments/main/openapi/shift4-api-openapi.yml
categories:
- shift4
description: Spectral linting rules defining API design standards and conventions for Shift4 Payments.
layout: rules
name: Shift4 Payments API Rules
provider_name: Shift4 Payments
provider_slug: shift4-payments
rule_count: 15
rules:
- description: All Shift4 operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: shift4-operation-id-required
  severity: error
- description: Shift4 operationIds use camelCase (e.g., createCharge, listEvents).
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: shift4-operation-id-camel-case
  severity: warn
- description: All Shift4 operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: shift4-tags-required
  severity: warn
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: shift4-summary-title-case
  severity: hint
- description: Shift4 paths are unversioned (no /v1/ prefix); the version lives in the secret key.
  given: $.paths[*]~
  name: shift4-no-versioned-paths
  severity: warn
- description: Shift4 paths must not have trailing slashes.
  given: $.paths[*]~
  name: shift4-no-trailing-slash
  severity: warn
- description: Shift4 uses HTTP Basic auth with the secret key as username.
  given: $.components.securitySchemes
  name: shift4-basic-auth-defined
  severity: error
- description: The Shift4 production server must be https://api.shift4.com.
  given: $.servers[*].url
  name: shift4-server-production
  severity: warn
- description: Amount fields must be integers expressed in the smallest currency unit.
  given: $.components.schemas[*].properties.amount.type
  name: shift4-amount-integer
  severity: warn
- description: Currency must be a string (ISO 4217 code).
  given: $.components.schemas[*].properties.currency.type
  name: shift4-currency-string
  severity: warn
- description: Resource 'created' timestamps are Unix seconds (integer int64).
  given: $.components.schemas[*].properties.created
  name: shift4-created-int64
  severity: hint
- description: All Shift4 operations should define a 200 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: shift4-response-200-defined
  severity: warn
- description: List endpoints should use a list/hasMore/totalCount envelope.
  given: $.components.schemas[?(@property.match(/^ListResponse/))].properties
  name: shift4-list-response-shape
  severity: hint
- description: Shift4 OpenAPI specs must include contact info.
  given: $.info
  name: shift4-info-contact
  severity: warn
- description: Shift4 API must define at least one server.
  given: $
  name: shift4-servers-defined
  severity: error
rules_file: rules/shift4-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shift4-payments/refs/heads/main/rules/shift4-api-rules.yml
severity_counts:
  error: 3
  hint: 3
  info: 0
  warn: 9
slug: shift4-api-rules
source_filename: shift4-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shift4-operation-id-required:\n    description: All Shift4 operations must have an operationId.\n    message: \"Operation at {{path}} is missing operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  shift4-operation-id-camel-case:\n    description: Shift4 operationIds use camelCase (e.g., createCharge, listEvents).\n    message: \"operationId '{{value}}' should use camelCase\"\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  shift4-tags-required:\n    description: All Shift4 operations must declare at least one tag.\n    message: \"Operation '{{path}}' must include at least one tag\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  shift4-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    severity: hint\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  shift4-no-versioned-paths:\n    description: Shift4 paths are unversioned (no /v1/ prefix); the version lives in the secret key.\n    message: \"Path '{{property}}' must not include a version prefix\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/v[0-9]+/\"\n\n  shift4-no-trailing-slash:\n    description: Shift4 paths must not have trailing slashes.\n    message: \"Path '{{property}}' must not end with a slash\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  shift4-basic-auth-defined:\n\
  \    description: Shift4 uses HTTP Basic auth with the secret key as username.\n    message: \"API must declare BasicAuth security scheme\"\n    given: \"$.components.securitySchemes\"\n    severity: error\n    then:\n      field: BasicAuth\n      function: truthy\n\n  shift4-server-production:\n    description: The Shift4 production server must be https://api.shift4.com.\n    message: \"Servers list should include https://api.shift4.com\"\n    given: \"$.servers[*].url\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.shift4\\\\.com$\"\n\n  shift4-amount-integer:\n    description: Amount fields must be integers expressed in the smallest currency unit.\n    message: \"amount field at '{{path}}' must be type integer\"\n    given: \"$.components.schemas[*].properties.amount.type\"\n    severity: warn\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  shift4-currency-string:\n\
  \    description: Currency must be a string (ISO 4217 code).\n    message: \"currency field at '{{path}}' must be type string\"\n    given: \"$.components.schemas[*].properties.currency.type\"\n    severity: warn\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  shift4-created-int64:\n    description: Resource 'created' timestamps are Unix seconds (integer int64).\n    message: \"created field at '{{path}}' should be int64 integer\"\n    given: \"$.components.schemas[*].properties.created\"\n    severity: hint\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type: { const: integer }\n            format: { const: int64 }\n\n  shift4-response-200-defined:\n    description: All Shift4 operations should define a 200 response.\n    message: \"Operation '{{path}}' should define a 200 success response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    severity: warn\n    then:\n      field: \"200\"\n      function: truthy\n\n  shift4-list-response-shape:\n    description: List endpoints should use a list/hasMore/totalCount envelope.\n    message: \"List response schema at '{{path}}' should include list, hasMore, totalCount\"\n    given: \"$.components.schemas[?(@property.match(/^ListResponse/))].properties\"\n    severity: hint\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [list, hasMore]\n\n  shift4-info-contact:\n    description: Shift4 OpenAPI specs must include contact info.\n    message: \"Info object must include contact details\"\n    given: \"$.info\"\n    severity: warn\n    then:\n      field: contact\n      function: truthy\n\n  shift4-servers-defined:\n    description: Shift4 API must define at least one server.\n    message: \"API must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n   \
  \   function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shift4-payments/refs/heads/main/rules/shift4-api-rules.yml
tags:
- Payments
- Fintech
- Commerce
- Checkout
- Spectral
- Linting
- API Governance
---
