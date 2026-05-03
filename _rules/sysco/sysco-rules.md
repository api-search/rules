---
api_specs:
- filename: sysco-food-distribution-api-openapi.yml
  format: yaml
  label: Sysco Food Distribution API
  slug: food-distribution-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sysco/refs/heads/main/openapi/sysco-food-distribution-api-openapi.yml
categories:
- delivery
- list
- operation
- order
- paths
- post
- product
- response
description: Spectral linting rules defining API design standards and conventions for Sysco.
layout: rules
name: Sysco API Rules
provider_name: Sysco
provider_slug: sysco
rule_count: 13
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: Product schema must include a productId (SUPC) field.
  given: $.components.schemas.Product.properties
  name: product-supc-field
  severity: error
- description: Order schema must include a deliveryDate field.
  given: $.components.schemas.Order.properties
  name: order-delivery-date
  severity: error
- description: OrderItem schema must include a quantity field.
  given: $.components.schemas.OrderItem.properties
  name: order-item-quantity
  severity: error
- description: List operations should support page parameter for pagination.
  given: $.paths[*].get
  name: list-pagination-page
  severity: warn
- description: Response schemas should use $ref for maintainability.
  given: $.paths[*][*].responses['200'].content['application/json'].schema
  name: response-schema-ref
  severity: info
- description: POST operations must include a request body.
  given: $.paths[*].post
  name: post-request-body
  severity: error
- description: Path segments must use kebab-case (lowercase with hyphens).
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Delivery schema should include estimatedArrival for tracking.
  given: $.components.schemas.Delivery.properties
  name: delivery-eta-field
  severity: warn
rules_file: rules/sysco-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sysco/refs/heads/main/rules/sysco-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 6
slug: sysco-rules
source_filename: sysco-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Require operationId\n  operation-operationId:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require summary\n  operation-summary:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Enforce Title Case on summaries\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Require tags on all operations\n  operation-tags:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # Require description on operations\n  operation-description:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Products must include SUPC field\n  product-supc-field:\n    description: Product schema must include a productId (SUPC) field.\n    severity: error\n    given: \"$.components.schemas.Product.properties\"\n    then:\n      field: productId\n      function: truthy\n\n  # Orders must include deliveryDate\n  order-delivery-date:\n    description: Order schema must include a deliveryDate field.\n    severity: error\n    given: \"$.components.schemas.Order.properties\"\n    then:\n      field: deliveryDate\n      function: truthy\n\n  # Order items must have required quantity\n  order-item-quantity:\n    description: OrderItem schema must include a quantity field.\n    severity:\
  \ error\n    given: \"$.components.schemas.OrderItem.properties\"\n    then:\n      field: quantity\n      function: truthy\n\n  # List operations must support pagination\n  list-pagination-page:\n    description: List operations should support page parameter for pagination.\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  # Response schemas should be referenced\n  response-schema-ref:\n    description: Response schemas should use $ref for maintainability.\n    severity: info\n    given: \"$.paths[*][*].responses['200'].content['application/json'].schema\"\n    then:\n      function: truthy\n\n  # POST operations must have request body\n  post-request-body:\n    description: POST operations must include a request body.\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Paths must use kebab-case\n  paths-kebab-case:\n    description: Path segments must\
  \ use kebab-case (lowercase with hyphens).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  # Delivery tracking should include estimatedArrival\n  delivery-eta-field:\n    description: Delivery schema should include estimatedArrival for tracking.\n    severity: warn\n    given: \"$.components.schemas.Delivery.properties\"\n    then:\n      field: estimatedArrival\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sysco/refs/heads/main/rules/sysco-rules.yml
tags:
- Food Distribution
- Food Service
- Supply Chain
- Fortune 100
- Wholesale
- Spectral
- Linting
- API Governance
---
