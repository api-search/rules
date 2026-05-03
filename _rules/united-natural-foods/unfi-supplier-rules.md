---
api_specs:
- filename: unfi-supplier-openapi.yml
  format: yaml
  label: UNFI Harmony Core API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-natural-foods/main/openapi/unfi-supplier-openapi.yml
categories:
- info
- list
- operation
- parameter
- path
- product
- response
- security
- servers
- unfi
description: Spectral linting rules defining API design standards and conventions for United Natural Foods (UNFI).
layout: rules
name: United Natural Foods (UNFI) API Rules
provider_name: United Natural Foods (UNFI)
provider_slug: united-natural-foods
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
- description: UNFI APIs use X-API-Key authentication. Security must be defined.
  given: $.paths.*[get,post,put,patch,delete]
  name: security-apikey-required
  severity: error
- description: POST, PUT, and PATCH operations should have a requestBody.
  given: $.paths.*[post,put,patch]
  name: operation-request-body-required
  severity: warn
- description: GET operations on collections should support page and pageSize parameters.
  given: $.paths.*[?(@parentProperty.match(/^\/(products|orders|insights)$/))]
  name: list-operation-pagination
  severity: info
- description: UNFI product ID examples should follow the UNFI-XXXXXXX format.
  given: $.components.schemas.Product.properties.productId.description
  name: unfi-product-id-format
  severity: info
- description: Product UPC should be exactly 12 numeric digits.
  given: $.components.schemas.Product.properties.upc
  name: product-upc-format
  severity: warn
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
rules_file: rules/unfi-supplier-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-natural-foods/refs/heads/main/rules/unfi-supplier-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 9
slug: unfi-supplier-rules
source_filename: unfi-supplier-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Require operationId on every operation\n  operation-operationId:\n    description: Every operation must have a unique operationId.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require operation summary in Title Case\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Require tags on every operation\n  operation-tags:\n    description: Every operation must include at least one tag.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Require description on every operation\n\
  \  operation-description:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Paths must use kebab-case\n  path-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens).\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  # Paths must not have a trailing slash\n  path-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  # All response codes must have descriptions\n  response-descriptions:\n    description: All response status codes must include a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].responses.*\"\n \
  \   then:\n      field: description\n      function: truthy\n\n  # API must use API key authentication\n  security-apikey-required:\n    description: UNFI APIs use X-API-Key authentication. Security must be defined.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # POST/PUT/PATCH must have a requestBody\n  operation-request-body-required:\n    description: POST, PUT, and PATCH operations should have a requestBody.\n    severity: warn\n    given: \"$.paths.*[post,put,patch]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Pagination parameters on list operations\n  list-operation-pagination:\n    description: GET operations on collections should support page and pageSize parameters.\n    message: \"List operation '{{path}}' should include pagination parameters.\"\n    severity: info\n    given: \"$.paths.*[?(@parentProperty.match(/^\\\\/(products|orders|insights)$/))]\"\n    then:\n\
  \      field: parameters\n      function: truthy\n\n  # UNFI product IDs follow UNFI-XXXXXXX format\n  unfi-product-id-format:\n    description: UNFI product ID examples should follow the UNFI-XXXXXXX format.\n    severity: info\n    given: \"$.components.schemas.Product.properties.productId.description\"\n    then:\n      function: truthy\n\n  # UPC must be 12 digits\n  product-upc-format:\n    description: Product UPC should be exactly 12 numeric digits.\n    severity: warn\n    given: \"$.components.schemas.Product.properties.upc\"\n    then:\n      field: description\n      function: truthy\n\n  # Require info contact\n  info-contact:\n    description: API info must include contact information.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # Servers must be defined\n  servers-defined:\n    description: API must define at least one server.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function:\
  \ truthy\n\n  # Parameters must have descriptions\n  parameter-description:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].parameters.*\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-natural-foods/refs/heads/main/rules/unfi-supplier-rules.yml
tags:
- Food Distribution
- Wholesale
- Natural Foods
- Supply Chain
- Fortune 500
- Spectral
- Linting
- API Governance
---
