---
api_specs:
- filename: waste-management-customer-api-openapi.yml
  format: yaml
  label: Waste Management Customer API
  slug: waste-management-customer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/waste-management/refs/heads/main/openapi/waste-management-customer-api-openapi.yml
categories:
- wm
description: Spectral linting rules defining API design standards and conventions for Waste Management.
layout: rules
name: Waste Management API Rules
provider_name: Waste Management
provider_slug: waste-management
rule_count: 8
rules:
- description: All operations must accept a Request-Tracking-Id header parameter.
  given: $.paths[*][get,post,put,patch,delete]
  name: wm-required-request-tracking-header
  severity: error
- description: All operations must accept a ClientId header parameter.
  given: $.paths[*][get,post,put,patch,delete]
  name: wm-required-client-id-header
  severity: error
- description: All WM API operations must declare bearerAuth security.
  given: $.paths[*][get,post,put,patch,delete]
  name: wm-bearer-auth-required
  severity: error
- description: Path parameters for customer identifiers must be named customerId.
  given: $.paths['/customers/{customerId}*'][*].parameters[?(@.in == 'path')]
  name: wm-customer-id-path-param-name
  severity: warning
- description: All authenticated operations must document a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wm-401-response-required
  severity: warning
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: wm-operation-id-camel-case
  severity: warning
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: wm-summary-title-case
  severity: info
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: wm-https-servers
  severity: error
rules_file: rules/waste-management-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/waste-management/refs/heads/main/rules/waste-management-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 0
  warning: 3
slug: waste-management-rules
source_filename: waste-management-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # WM API requires Request-Tracking-Id and ClientId headers on all operations\n  wm-required-request-tracking-header:\n    description: All operations must accept a Request-Tracking-Id header parameter.\n    message: \"Operation '{{title}}' is missing the required Request-Tracking-Id header parameter.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: Request-Tracking-Id\n              in:\n                const: header\n\n  wm-required-client-id-header:\n    description: All operations must accept a ClientId header parameter.\n    message: \"Operation '{{title}}' is missing the required ClientId header parameter.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: ClientId\n              in:\n                const: header\n\n  # WM API uses JWT bearer auth — all operations must declare security\n  wm-bearer-auth-required:\n    description: All WM API operations must declare bearerAuth security.\n    message: \"Operation '{{title}}' must declare bearerAuth security requirement.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # Customer ID path parameter must be named customerId\n  wm-customer-id-path-param-name:\n    description: Path parameters for customer identifiers must be named customerId.\n    message: \"Customer path parameters should be named 'customerId'.\"\n    severity: warning\n    given: \"$.paths['/customers/{customerId}*'][*].parameters[?(@.in\
  \ == 'path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - customerId\n          - serviceId\n          - invoiceId\n\n  # All responses must include 401 Unauthorized\n  wm-401-response-required:\n    description: All authenticated operations must document a 401 Unauthorized response.\n    message: \"Operation '{{title}}' is missing a 401 Unauthorized response.\"\n    severity: warning\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  # Operation IDs must use camelCase\n  wm-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warning\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  # Summaries must use Title Case\n  wm-summary-title-case:\n    description:\
  \ Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: info\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # API servers must use HTTPS\n  wm-https-servers:\n    description: All server URLs must use HTTPS.\n    message: \"Server URL '{{value}}' must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/waste-management/refs/heads/main/rules/waste-management-rules.yml
tags:
- Environmental Services
- Fortune 500
- Recycling
- Solid Waste
- Sustainability
- Waste Management
- Spectral
- Linting
- API Governance
---
