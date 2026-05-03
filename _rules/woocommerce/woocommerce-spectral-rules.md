---
api_specs:
- filename: woocommerce-rest-api-openapi.yml
  format: yaml
  label: WooCommerce REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/woocommerce/refs/heads/main/openapi/woocommerce-rest-api-openapi.yml
- filename: woocommerce-store-api-openapi.yml
  format: yaml
  label: WooCommerce Store API
  slug: store-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/woocommerce/refs/heads/main/openapi/woocommerce-store-api-openapi.yml
- filename: woocommerce-webhooks-asyncapi.yml
  format: yaml
  label: WooCommerce Webhook Events
  slug: webhook-events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/woocommerce/refs/heads/main/asyncapi/woocommerce-webhooks-asyncapi.yml
categories:
- delete
- external
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- post
- put
- request
- response
- schema
- security
- servers
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for WooCommerce.
layout: rules
name: WooCommerce API Rules
provider_name: WooCommerce
provider_slug: woocommerce
rule_count: 37
rules:
- description: API title must be present and start with "WooCommerce".
  given: $.info
  name: info-title-required
  severity: error
- description: API description must be present and at least 100 characters.
  given: $.info
  name: info-description-required
  severity: error
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information must be present.
  given: $.info
  name: info-contact-required
  severity: warn
- description: Terms of service URL must be present.
  given: $.info
  name: info-terms-of-service
  severity: warn
- description: OpenAPI version must be 3.1.0.
  given: $
  name: openapi-version-31
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-required
  severity: error
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments must use kebab-case (lowercase letters, digits, hyphens).
  given: $.paths[*]~
  name: paths-use-kebab-case
  severity: warn
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Collection resource paths should use plural nouns.
  given: $.paths[*]~
  name: paths-plural-resource-nouns
  severity: info
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationid-camelcase
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "WooCommerce ".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-woocommerce-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: All parameters must have descriptions.
  given: $.paths[*][get,post,put,patch,delete][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameter names must use snake_case.
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameter-naming-snake-case
  severity: warn
- description: Pagination parameters should be named page and per_page.
  given: $.paths[*][get].parameters[*]
  name: parameter-pagination-standard
  severity: info
- description: Request bodies should use application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content-type
  severity: warn
- description: Operations must define at least a 200 or 201 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have descriptions.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Successful responses should return application/json.
  given: $.paths[*][get,post,put,patch].responses['200'].content
  name: response-json-content-type
  severity: warn
- description: Protected endpoints should define a 401 unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-error-401-defined
  severity: info
- description: Schema property names must use snake_case.
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: warn
- description: Top-level component schemas should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schemas should define an explicit type.
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: GET operations must not have request bodies.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 200 or 204.
  given: $.paths[*].delete.responses
  name: delete-returns-200-or-204
  severity: warn
- description: POST operations that create resources should have request bodies.
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: PUT operations must have request bodies.
  given: $.paths[*].put
  name: put-has-request-body
  severity: error
- description: Global tags array should be defined with all tags used in operations.
  given: $
  name: tags-global-defined
  severity: warn
- description: Global tag definitions must include descriptions.
  given: $.tags[*]
  name: tag-descriptions-required
  severity: warn
- description: Operations should include x-microcks-operation for mock server compatibility.
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
- description: APIs should reference external documentation.
  given: $
  name: external-docs-encouraged
  severity: info
rules_file: rules/woocommerce-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/woocommerce/refs/heads/main/rules/woocommerce-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 5
  warn: 21
slug: woocommerce-spectral-rules
source_filename: woocommerce-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and start with \"WooCommerce\".\n    message: \"info.title must be present and start with 'WooCommerce'.\"\n    severity: error\n    given: $.info\n    then:\n      - field: title\n        function: truthy\n      - field: title\n        function: pattern\n        functionOptions:\n          match: \"^WooCommerce\"\n\n  info-description-required:\n    description: API description must be present and at least 100 characters.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        value: 100\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information must be present.\n    severity: warn\n    given: $.info\n    then:\n      field:\
  \ contact\n      function: truthy\n\n  info-terms-of-service:\n    description: Terms of service URL must be present.\n    severity: warn\n    given: $.info\n    then:\n      field: termsOfService\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-31:\n    description: OpenAPI version must be 3.1.0.\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-description-required:\n    description: Each server should have a description.\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # PATHS - NAMING CONVENTIONS\n  paths-use-kebab-case:\n    description: Path segments must use kebab-case (lowercase letters, digits, hyphens).\n  \
  \  severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/([a-z0-9][a-z0-9-]*[a-z0-9]|[a-z0-9]|\\\\{[a-z_]+\\\\}|wc/v[0-9]|wc/store/v[0-9]))*$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-plural-resource-nouns:\n    description: Collection resource paths should use plural nouns.\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/(product|order|customer|coupon|webhook|setting|tax-rate|shipping-zone|payment-gateway)$\"\n\n  # OPERATIONS\n  operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camelcase:\n\
  \    description: operationId must use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-woocommerce-prefix:\n    description: Operation summaries must start with \"WooCommerce \".\n    message: \"Operation summary must start with 'WooCommerce '.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^WooCommerce \"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n  \
  \    field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have descriptions.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-naming-snake-case:\n    description: Parameter names must use snake_case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  parameter-pagination-standard:\n    description: Pagination parameters should be named page and per_page.\n    severity: info\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n\
  \      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                pattern: \"page\"\n          then:\n            properties:\n              name:\n                enum: [page, per_page]\n\n  # REQUEST BODIES\n  request-body-json-content-type:\n    description: Request bodies should use application/json content type.\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['application/json']\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  response-description-required:\n\
  \    description: All responses must have descriptions.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  response-json-content-type:\n    description: Successful responses should return application/json.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses['200'].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['application/json']\n\n  response-error-401-defined:\n    description: Protected endpoints should define a 401 unauthorized response.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['401']\n            - required: ['403']\n\n  # SCHEMAS - PROPERTY NAMING\n  schema-property-snake-case:\n    description: Schema property names must use snake_case.\n\
  \    severity: warn\n    given: \"$.components.schemas[*].properties[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  schema-description-required:\n    description: Top-level component schemas should have descriptions.\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-type-defined:\n    description: Schemas should define an explicit type.\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: type\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have request bodies.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n\
  \      function: falsy\n\n  delete-returns-200-or-204:\n    description: DELETE operations should return 200 or 204.\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['204']\n\n  post-has-request-body:\n    description: POST operations that create resources should have request bodies.\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  put-has-request-body:\n    description: PUT operations must have request bodies.\n    severity: error\n    given: \"$.paths[*].put\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # GENERAL QUALITY\n  tags-global-defined:\n    description: Global tags array should be defined with all tags used in operations.\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  tag-descriptions-required:\n\
  \    description: Global tag definitions must include descriptions.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  microcks-operation-extension:\n    description: Operations should include x-microcks-operation for mock server compatibility.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  external-docs-encouraged:\n    description: APIs should reference external documentation.\n    severity: info\n    given: $\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/woocommerce/refs/heads/main/rules/woocommerce-spectral-rules.yml
tags:
- eCommerce
- Open Source
- Orders
- Products
- WordPress
- Spectral
- Linting
- API Governance
---
