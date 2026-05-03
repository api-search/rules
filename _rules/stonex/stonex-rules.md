---
api_specs:
- filename: stonex-payments-openapi.yml
  format: yaml
  label: StoneX Payments API
  slug: stonex-payments
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stonex/refs/heads/main/openapi/stonex-payments-openapi.yml
- filename: stonex-clearing-openapi.yml
  format: yaml
  label: StoneX Clearing API
  slug: stonex-clearing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stonex/refs/heads/main/openapi/stonex-clearing-openapi.yml
categories:
- stonex
description: Spectral linting rules defining API design standards and conventions for StoneX.
layout: rules
name: StoneX API Rules
provider_name: StoneX
provider_slug: stonex
rule_count: 7
rules:
- description: All StoneX API operations must use Bearer JWT authentication.
  given: $.components.securitySchemes
  name: stonex-bearer-auth-required
  severity: error
- description: All StoneX operations must define a 2xx success response.
  given: $.paths[*][*]
  name: stonex-response-200-or-201-required
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: stonex-operationid-camel-case
  severity: warn
- description: All operation tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: stonex-tags-title-case
  severity: warn
- description: All StoneX API servers must use HTTPS with TLS 1.3.
  given: $.servers[*].url
  name: stonex-server-https
  severity: error
- description: Currency parameters must reference ISO 4217 in their description to ensure standardized currency code usage.
  given: $.paths[*][*].parameters[?(@.name =~ /currency/i)]
  name: stonex-iso-currency-description
  severity: info
- description: Path segments (not parameters) should use kebab-case.
  given: $.paths[*]~
  name: stonex-path-parameters-kebab-case
  severity: warn
rules_file: rules/stonex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stonex/refs/heads/main/rules/stonex-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: stonex-rules
source_filename: stonex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stonex-bearer-auth-required:\n    description: >-\n      All StoneX API operations must use Bearer JWT authentication.\n    message: \"Operations must declare BearerAuth security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: defined\n\n  stonex-response-200-or-201-required:\n    description: All StoneX operations must define a 2xx success response.\n    message: \"Operation must define a 200 or 201 response.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            responses:\n              type: object\n\n  stonex-operationid-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stonex-tags-title-case:\n    description: All operation tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]*$\"\n\n  stonex-server-https:\n    description: All StoneX API servers must use HTTPS with TLS 1.3.\n    message: \"Server URL must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  stonex-iso-currency-description:\n    description: >-\n      Currency parameters must reference ISO 4217 in their description\n      to ensure standardized currency code usage.\n    message: \"Currency parameter must mention ISO 4217.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name =~ /currency/i)]\"\n    then:\n      field: description\n    \
  \  function: truthy\n\n  stonex-path-parameters-kebab-case:\n    description: Path segments (not parameters) should use kebab-case.\n    message: \"Path '{{path}}' contains uppercase characters.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9{}_-]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stonex/refs/heads/main/rules/stonex-rules.yml
tags:
- Finance
- Financial Services
- Payments
- Clearing
- Futures
- Trading
- Risk Management
- Spectral
- Linting
- API Governance
---
