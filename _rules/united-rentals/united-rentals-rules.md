---
api_specs:
- filename: united-rentals-total-control-openapi.yml
  format: yaml
  label: United Rentals Total Control Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-rentals/main/openapi/united-rentals-total-control-openapi.yml
categories:
- date
- equipment
- info
- operation
- parameter
- path
- rental
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for United Rentals.
layout: rules
name: United Rentals API Rules
provider_name: United Rentals
provider_slug: united-rentals
rule_count: 15
rules:
- description: Every operation must have a unique operationId.
  given: $.paths.*[get,post,put,patch,delete,options,head]
  name: operation-operationId
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must include at least one tag.
  given: $.paths.*[get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: Every operation must have a description.
  given: $.paths.*[get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: Path segments must use kebab-case (lowercase with hyphens).
  given: $.paths[*]~
  name: path-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: path-no-trailing-slash
  severity: error
- description: All response status codes must include a description.
  given: $.paths.*[get,post,put,patch,delete].responses.*
  name: response-descriptions
  severity: warn
- description: United Rentals APIs require X-API-Key authentication. Security must be defined on all operations.
  given: $.paths.*[get,post,put,patch,delete]
  name: security-apikey-required
  severity: error
- description: POST, PUT, and PATCH operations should have a requestBody.
  given: $.paths.*[post,put,patch]
  name: operation-request-body-required
  severity: warn
- description: Date fields must use format date (ISO 8601 YYYY-MM-DD).
  given: $.components.schemas.*[*]
  name: date-field-format
  severity: error
- description: Rental creation requires a purchaseOrderNumber for ERP integration.
  given: $.components.schemas.RentalRequest.required
  name: rental-purchase-order-required
  severity: error
- description: API info must include contact information.
  given: $.info
  name: info-contact
  severity: warn
- description: API must define at least one server.
  given: $
  name: servers-defined
  severity: error
- description: All parameters must have a description.
  given: $.paths.*[get,post,put,patch,delete].parameters.*
  name: parameter-description
  severity: warn
- description: Equipment schemas should define dailyRate, weeklyRate, and monthlyRate.
  given: $.components.schemas.Equipment.properties
  name: equipment-rate-completeness
  severity: warn
rules_file: rules/united-rentals-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-rentals/refs/heads/main/rules/united-rentals-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 9
slug: united-rentals-rules
source_filename: united-rentals-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Require operationId on every operation\n  operation-operationId:\n    description: Every operation must have a unique operationId.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require operation summary in Title Case\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Require tags on every operation\n  operation-tags:\n    description: Every operation must include at least one tag.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Require description on every operation\n\
  \  operation-description:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Paths must use kebab-case\n  path-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens).\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  # Paths must not have a trailing slash\n  path-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  # All response codes must have descriptions\n  response-descriptions:\n    description: All response status codes must include a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].responses.*\"\n \
  \   then:\n      field: description\n      function: truthy\n\n  # API must use API key authentication (Total Control platform)\n  security-apikey-required:\n    description: United Rentals APIs require X-API-Key authentication. Security must be defined on all operations.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # POST/PUT/PATCH must have a requestBody\n  operation-request-body-required:\n    description: POST, PUT, and PATCH operations should have a requestBody.\n    severity: warn\n    given: \"$.paths.*[post,put,patch]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Rental dates must use ISO 8601 date format\n  date-field-format:\n    description: Date fields must use format date (ISO 8601 YYYY-MM-DD).\n    severity: error\n    given: \"$.components.schemas.*[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n           \
  \ properties:\n              type:\n                const: string\n            required: [type]\n          then:\n            not:\n              properties:\n                description:\n                  pattern: \"date\"\n\n  # Purchase order number is required for rental creation\n  rental-purchase-order-required:\n    description: Rental creation requires a purchaseOrderNumber for ERP integration.\n    severity: error\n    given: \"$.components.schemas.RentalRequest.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: purchaseOrderNumber\n\n  # API info must include contact information\n  info-contact:\n    description: API info must include contact information.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # Servers must be defined\n  servers-defined:\n    description: API must define at least one server.\n    severity: error\n\
  \    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  # Parameters must have descriptions\n  parameter-description:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].parameters.*\"\n    then:\n      field: description\n      function: truthy\n\n  # Equipment rental rates must include daily, weekly, and monthly\n  equipment-rate-completeness:\n    description: Equipment schemas should define dailyRate, weeklyRate, and monthlyRate.\n    severity: warn\n    given: \"$.components.schemas.Equipment.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [dailyRate, weeklyRate, monthlyRate]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-rentals/refs/heads/main/rules/united-rentals-rules.yml
tags:
- Equipment Rental
- Procurement
- Supply Chain
- Construction
- Fortune 500
- Spectral
- Linting
- API Governance
---
