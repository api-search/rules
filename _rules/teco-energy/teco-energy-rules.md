---
api_specs:
- filename: teco-energy-outage-openapi.yml
  format: yaml
  label: Tampa Electric Outage API
  slug: outage-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/teco-energy/refs/heads/main/openapi/teco-energy-outage-openapi.yml
- filename: teco-energy-account-openapi.yml
  format: yaml
  label: Tampa Electric Account API
  slug: account-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/teco-energy/refs/heads/main/openapi/teco-energy-account-openapi.yml
categories:
- teco
description: Spectral linting rules defining API design standards and conventions for TECO Energy.
layout: rules
name: TECO Energy API Rules
provider_name: TECO Energy
provider_slug: teco-energy
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: teco-energy-operation-ids-camel-case
  severity: warn
- description: All non-public endpoints must use bearer authentication.
  given: $.paths[*][*]
  name: teco-energy-bearer-auth-required
  severity: warn
- description: All responses must have descriptions.
  given: $.paths[*][*].responses[*]
  name: teco-energy-responses-have-descriptions
  severity: error
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: teco-energy-operations-have-tags
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: teco-energy-operations-have-summaries
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: teco-energy-title-case-summaries
  severity: warn
- description: Account-scoped operations must use accountNumber path parameter.
  given: $.paths['/accounts/{accountNumber}'][*].parameters[*]
  name: teco-energy-account-number-in-path
  severity: hint
- description: API must define at least one server.
  given: $
  name: teco-energy-servers-defined
  severity: error
- description: API must define reusable schemas in components.
  given: $.components
  name: teco-energy-components-schemas
  severity: warn
- description: API must define security schemes.
  given: $.components
  name: teco-energy-security-schemes-defined
  severity: error
rules_file: rules/teco-energy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/teco-energy/refs/heads/main/rules/teco-energy-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 5
slug: teco-energy-rules
source_filename: teco-energy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  teco-energy-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  teco-energy-bearer-auth-required:\n    description: All non-public endpoints must use bearer authentication.\n    message: \"Operation should define bearer security scheme.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  teco-energy-responses-have-descriptions:\n    description: All responses must have descriptions.\n    message: \"Response must include a description.\"\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  teco-energy-operations-have-tags:\n    description:\
  \ All operations must be tagged.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  teco-energy-operations-have-summaries:\n    description: All operations must have a summary.\n    message: \"Operation must include a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  teco-energy-title-case-summaries:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  teco-energy-account-number-in-path:\n    description: Account-scoped operations must use accountNumber path parameter.\n    message: \"Account endpoints should use 'accountNumber' as the path parameter name.\"\n    severity: hint\n\
  \    given: \"$.paths['/accounts/{accountNumber}'][*].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  teco-energy-servers-defined:\n    description: API must define at least one server.\n    message: \"API must include a servers array.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  teco-energy-components-schemas:\n    description: API must define reusable schemas in components.\n    message: \"API should define schemas in components/schemas.\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n\n  teco-energy-security-schemes-defined:\n    description: API must define security schemes.\n    message: \"API must define security schemes in components/securitySchemes.\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/teco-energy/refs/heads/main/rules/teco-energy-rules.yml
tags:
- Energy
- Utilities
- Electric
- Natural Gas
- Smart Grid
- Tampa Bay
- Spectral
- Linting
- API Governance
---
