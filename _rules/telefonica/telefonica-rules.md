---
api_specs:
- filename: telefonica-number-verification-openapi.yml
  format: yaml
  label: Telefónica Number Verification API
  slug: number-verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-number-verification-openapi.yml
- filename: telefonica-sim-swap-openapi.yml
  format: yaml
  label: Telefónica SIM Swap API
  slug: sim-swap-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-sim-swap-openapi.yml
- filename: telefonica-kyc-match-openapi.yml
  format: yaml
  label: Telefónica Know Your Customer Match API
  slug: kyc-match-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-kyc-match-openapi.yml
- filename: telefonica-location-verification-openapi.yml
  format: yaml
  label: Telefónica Location Verification API
  slug: location-verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-location-verification-openapi.yml
- filename: telefonica-quality-on-demand-openapi.yml
  format: yaml
  label: Telefónica Quality on Demand API
  slug: quality-on-demand-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-quality-on-demand-openapi.yml
- filename: telefonica-device-roaming-openapi.yml
  format: yaml
  label: Telefónica Device Roaming Status API
  slug: device-roaming-status-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/openapi/telefonica-device-roaming-openapi.yml
categories:
- telefonica
description: Spectral linting rules defining API design standards and conventions for Telefónica.
layout: rules
name: Telefónica API Rules
provider_name: Telefónica
provider_slug: telefonica
rule_count: 11
rules:
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: telefonica-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: telefonica-operations-have-summaries
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: telefonica-title-case-summaries
  severity: warn
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: telefonica-operations-have-tags
  severity: warn
- description: All responses must have descriptions.
  given: $.paths[*][*].responses[*]
  name: telefonica-responses-have-descriptions
  severity: error
- description: Telefónica Open Gateway APIs must use OpenID Connect authentication.
  given: $.components.securitySchemes[*]
  name: telefonica-openid-security-scheme
  severity: warn
- description: Phone number fields must use E.164 format pattern.
  given: $.components.schemas[*].properties.phoneNumber
  name: telefonica-phone-number-e164-pattern
  severity: warn
- description: Error responses must define a schema.
  given: $.paths[*][*].responses[4*].content.application/json
  name: telefonica-error-response-schema
  severity: error
- description: API must define production and sandbox servers.
  given: $
  name: telefonica-servers-defined
  severity: error
- description: CAMARA APIs should include version information in info.
  given: $.info
  name: telefonica-camara-version
  severity: error
- description: Open Gateway APIs must include license information.
  given: $.info
  name: telefonica-license-defined
  severity: warn
rules_file: rules/telefonica-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/rules/telefonica-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 6
slug: telefonica-rules
source_filename: telefonica-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  telefonica-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telefonica-operations-have-summaries:\n    description: All operations must have a summary.\n    message: \"Operation must include a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  telefonica-title-case-summaries:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  telefonica-operations-have-tags:\n  \
  \  description: All operations must be tagged.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telefonica-responses-have-descriptions:\n    description: All responses must have descriptions.\n    message: \"Response must include a description.\"\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefonica-openid-security-scheme:\n    description: Telefónica Open Gateway APIs must use OpenID Connect authentication.\n    message: \"Security scheme should use OpenID Connect.\"\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - openIdConnect\n\n  telefonica-phone-number-e164-pattern:\n    description: Phone number fields must use E.164 format pattern.\n    message: \"\
  Phone number field should define E.164 pattern validation.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.phoneNumber\"\n    then:\n      field: pattern\n      function: truthy\n\n  telefonica-error-response-schema:\n    description: Error responses must define a schema.\n    message: \"Error response must include a schema.\"\n    severity: error\n    given: \"$.paths[*][*].responses[4*].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  telefonica-servers-defined:\n    description: API must define production and sandbox servers.\n    message: \"API must include a servers array.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  telefonica-camara-version:\n    description: CAMARA APIs should include version information in info.\n    message: \"API must define a version in info.version.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function:\
  \ truthy\n\n  telefonica-license-defined:\n    description: Open Gateway APIs must include license information.\n    message: \"API must define license information.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telefonica/refs/heads/main/rules/telefonica-rules.yml
tags:
- Telecommunications
- Mobile Network
- CAMARA
- Open Gateway
- Authentication
- Fraud Prevention
- Location Services
- Spectral
- Linting
- API Governance
---
