---
api_specs:
- filename: openapi.json
  format: json
  label: Temenos Transact API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.temenos.com/transact/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Infinity API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.temenos.com/infinity/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Payments API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.temenos.com/payments/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Fund Administration API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.temenos.com/funds/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Financial Crime Mitigation API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.temenos.com/fcm/openapi.json
- filename: temenos-data-hub-openapi.yml
  format: yaml
  label: Temenos Transact Data Hub API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-data-hub-openapi.yml
- filename: temenos-wealth-openapi.yml
  format: yaml
  label: Temenos Wealth API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-wealth-openapi.yml
- filename: temenos-enterprise-product-pricing-openapi.yml
  format: yaml
  label: Temenos Enterprise Product and Pricing API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-enterprise-product-pricing-openapi.yml
- filename: temenos-cloud-banking-openapi.yml
  format: yaml
  label: Temenos Cloud Banking (CMB) API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-cloud-banking-openapi.yml
- filename: temenos-journey-manager-openapi.yml
  format: yaml
  label: Temenos Journey Manager API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-journey-manager-openapi.yml
- filename: temenos-microservices-openapi.yml
  format: yaml
  label: Temenos Transact Microservices API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-microservices-openapi.yml
- filename: temenos-bnpl-openapi.yml
  format: yaml
  label: Temenos Buy Now Pay Later API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-bnpl-openapi.yml
categories:
- temenos
description: Spectral linting rules defining API design standards and conventions for Temenos.
layout: rules
name: Temenos API Rules
provider_name: Temenos
provider_slug: temenos
rule_count: 14
rules:
- description: All Temenos API operations must declare bearerAuth or oauth2 security
  given: $.paths[*][get,post,put,patch,delete]
  name: temenos-security-bearer-required
  severity: error
- description: OperationIds must use camelCase following Temenos convention
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: temenos-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: temenos-summary-title-case
  severity: warn
- description: All operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: temenos-operation-tags-required
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: temenos-operation-description-required
  severity: warn
- description: GET operations returning arrays should support page_size and page_start pagination
  given: $.paths[*].get
  name: temenos-get-list-pagination
  severity: info
- description: Currency fields should use ISO 4217 three-letter codes
  given: $.components.schemas[*].properties.currency
  name: temenos-currency-iso-format
  severity: info
- description: Operations should reference standard Temenos error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: temenos-standard-error-responses
  severity: warn
- description: GET operations for single resources should define 404 response
  given: $.paths[*~'\{[a-zA-Z]+\}$'].get.responses
  name: temenos-get-single-404-response
  severity: warn
- description: Path segments must use kebab-case (lowercase with hyphens)
  given: $.paths[*~'[A-Z_]']
  name: temenos-path-kebab-case
  severity: warn
- description: API spec must define at least one server URL
  given: $
  name: temenos-server-url-required
  severity: error
- description: API spec must include contact information
  given: $.info
  name: temenos-info-contact-required
  severity: warn
- description: API spec must include license information
  given: $.info
  name: temenos-info-license-required
  severity: warn
- description: Successful responses must include a response schema
  given: $.paths[*][get,post,put,patch].responses[200,201].content.application/json
  name: temenos-success-response-schema
  severity: warn
rules_file: rules/temenos-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/rules/temenos-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 10
slug: temenos-rules
source_filename: temenos-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Enforce Temenos bearer auth on all operations\n  temenos-security-bearer-required:\n    description: All Temenos API operations must declare bearerAuth or oauth2 security\n    message: \"Operation '{{operationId}}' is missing required Temenos security scheme (bearerAuth or oauth2)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # Enforce operation IDs in camelCase\n  temenos-operation-id-camel-case:\n    description: OperationIds must use camelCase following Temenos convention\n    message: \"operationId '{{value}}' should use camelCase (e.g. listAccounts, createPaymentOrder)\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Enforce Title Case summaries\n  temenos-summary-title-case:\n    description: Operation\
  \ summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Enforce tags on all operations\n  temenos-operation-tags-required:\n    description: All operations must have at least one tag for grouping\n    message: \"Operation '{{operationId}}' must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Enforce descriptions on all operations\n  temenos-operation-description-required:\n    description: All operations must have a description\n    message: \"Operation is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Enforce pagination parameters on GET\
  \ list operations\n  temenos-get-list-pagination:\n    description: GET operations returning arrays should support page_size and page_start pagination\n    message: \"List operation should include page_size and page_start query parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            operationId:\n              pattern: \"^list\"\n\n  # Enforce ISO 4217 currency codes\n  temenos-currency-iso-format:\n    description: Currency fields should use ISO 4217 three-letter codes\n    message: \"Currency schema should enforce ISO 4217 format with pattern '^[A-Z]{3}$'\"\n    severity: info\n    given: \"$.components.schemas[*].properties.currency\"\n    then:\n      field: pattern\n      function: truthy\n\n  # Enforce standard error response components\n  temenos-standard-error-responses:\n    description: Operations should reference standard Temenos error responses\n    message:\
  \ \"Operation should define 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Enforce 404 on GET single resource operations\n  temenos-get-single-404-response:\n    description: GET operations for single resources should define 404 response\n    message: \"Single resource GET should define a 404 Not Found response\"\n    severity: warn\n    given: \"$.paths[*~'\\\\{[a-zA-Z]+\\\\}$'].get.responses\"\n    then:\n      field: \"404\"\n      function: truthy\n\n  # Enforce kebab-case path segments\n  temenos-path-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens)\n    message: \"Path segment '{{value}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*~'[A-Z_]']\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z_]\"\n\n  # Enforce consistent server URLs\n  temenos-server-url-required:\n\
  \    description: API spec must define at least one server URL\n    message: \"API spec is missing server URLs\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  # Enforce contact information\n  temenos-info-contact-required:\n    description: API spec must include contact information\n    message: \"API spec is missing contact information in info\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # Enforce license information\n  temenos-info-license-required:\n    description: API spec must include license information\n    message: \"API spec is missing license information in info\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  # Enforce response schemas on 200/201 responses\n  temenos-success-response-schema:\n    description: Successful responses must include a response schema\n    message: \"200/201 response is missing\
  \ a schema definition\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses[200,201].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/rules/temenos-rules.yml
tags:
- Banking
- Cloud Banking
- Core Banking
- Digital Banking
- Financial Services
- Fintech
- Open Banking
- Payments
- Wealth Management
- Spectral
- Linting
- API Governance
---
