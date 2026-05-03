---
api_specs:
- filename: swift-swiftref-api-openapi.yml
  format: yaml
  label: SwiftRef API
  slug: swiftref-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swift/refs/heads/main/openapi/swift-swiftref-api-openapi.yml
categories:
- swift
description: Spectral linting rules defining API design standards and conventions for SWIFT.
layout: rules
name: SWIFT API Rules
provider_name: SWIFT
provider_slug: swift
rule_count: 8
rules:
- description: SWIFT API endpoints must use OAuth2 security scheme
  given: $.components.securitySchemes
  name: swift-oauth2-security
  severity: warn
- description: Financial identifier path parameters must have regex pattern validation
  given: $.components.parameters[?(@.in == 'path')].schema
  name: swift-identifier-pattern
  severity: warn
- description: SWIFT API paths should include version prefix (/v2/)
  given: $.paths
  name: swift-versioned-paths
  severity: warn
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][get,post,put,patch,delete]
  name: swift-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: swift-summary-title-case
  severity: warn
- description: Validation endpoints should return a validity result with a 'valid' boolean
  given: $.paths[?(@property.endsWith('validity'))].get.responses.200.content.application/json.schema
  name: swift-validity-response
  severity: hint
- description: GET lookup endpoints should document 404 responses
  given: $.paths[*].get.responses
  name: swift-not-found-response
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: swift-operation-tags
  severity: warn
rules_file: rules/swift-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/swift/refs/heads/main/rules/swift-rules.yml
severity_counts:
  error: 0
  hint: 1
  info: 0
  warn: 7
slug: swift-rules
source_filename: swift-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n  # SWIFT APIs use OAuth2 authentication\n  swift-oauth2-security:\n    description: SWIFT API endpoints must use OAuth2 security scheme\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: OAuth2\n      function: truthy\n\n  # All path parameters for financial identifiers must have patterns\n  swift-identifier-pattern:\n    description: Financial identifier path parameters must have regex pattern validation\n    severity: warn\n    given: \"$.components.parameters[?(@.in == 'path')].schema\"\n    then:\n      field: pattern\n      function: truthy\n\n  # All paths must be versioned with /v2/ prefix\n  swift-versioned-paths:\n    description: SWIFT API paths should include version prefix (/v2/)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  # Operation IDs must use camelCase\n  swift-operation-id-camel-case:\n\
  \    description: Operation IDs must use camelCase naming convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have summaries using Title Case\n  swift-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # GET endpoints for validation should return ValidityResult schema\n  swift-validity-response:\n    description: Validation endpoints should return a validity result with a 'valid' boolean\n    severity: hint\n    given: \"$.paths[?(@property.endsWith('validity'))].get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n \
  \         type: object\n          required:\n            - properties\n          properties:\n            properties:\n              type: object\n              required:\n                - valid\n\n  # 404 responses should be defined for lookup endpoints\n  swift-not-found-response:\n    description: GET lookup endpoints should document 404 responses\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: '404'\n      function: truthy\n\n  # Operations must have at least one tag\n  swift-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/swift/refs/heads/main/rules/swift-rules.yml
tags:
- Banking
- Cross-Border Payments
- Financial Messaging
- Financial Services
- GPI
- ISO 20022
- Payments
- Spectral
- Linting
- API Governance
---
