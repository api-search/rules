---
api_specs:
- filename: urban-outfitters-affiliate-api-openapi.yml
  format: yaml
  label: Urban Outfitters Affiliate Program
  slug: affiliate-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/urban-outfitters/refs/heads/main/openapi/urban-outfitters-affiliate-api-openapi.yml
- filename: urban-outfitters-marketplace-api-openapi.yml
  format: yaml
  label: Urban Outfitters Marketplace (UO MRKT) Integration
  slug: marketplace-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/urban-outfitters/refs/heads/main/openapi/urban-outfitters-marketplace-api-openapi.yml
categories:
- uo
description: Spectral linting rules defining API design standards and conventions for Urban Outfitters.
layout: rules
name: Urban Outfitters API Rules
provider_name: Urban Outfitters
provider_slug: urban-outfitters
rule_count: 31
rules:
- description: API info must have a title
  given: $.info
  name: uo-info-title-present
  severity: error
- description: API info must have a description
  given: $.info
  name: uo-info-description-present
  severity: warn
- description: API info must have a version
  given: $.info
  name: uo-info-version-present
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: uo-openapi-version
  severity: error
- description: API must define servers
  given: $
  name: uo-servers-present
  severity: warn
- description: Server URLs should use HTTPS
  given: $.servers[*].url
  name: uo-server-url-https
  severity: warn
- description: API must define paths
  given: $
  name: uo-paths-present
  severity: error
- description: Path segments should be lowercase
  given: $.paths[*]~
  name: uo-path-lowercase
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: uo-operation-id-present
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: uo-operation-summary-present
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: uo-operation-description-present
  severity: hint
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: uo-operation-tags-present
  severity: warn
- description: All tags used in operations should be defined at the top level
  given: $
  name: uo-tags-defined
  severity: warn
- description: All parameters should have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uo-parameter-description-present
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uo-parameter-schema-present
  severity: error
- description: Request bodies should have a description
  given: $.paths[*][post,put,patch].requestBody
  name: uo-request-body-description
  severity: hint
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: uo-response-description-present
  severity: error
- description: Operations must have at least one success (2xx) response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: uo-response-success-present
  severity: error
- description: Operations should define error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: uo-response-error-present
  severity: warn
- description: All schemas should have a description
  given: $.components.schemas[*]
  name: uo-schema-description-present
  severity: hint
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: uo-schema-properties-examples
  severity: hint
- description: API must define security schemes
  given: $.components
  name: uo-security-schemes-defined
  severity: error
- description: API should define global security requirements
  given: $
  name: uo-global-security-present
  severity: warn
- description: GET operations should not have a request body
  given: $.paths[*].get
  name: uo-get-no-request-body
  severity: warn
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: uo-delete-no-body
  severity: hint
- description: Affiliate product responses should include affiliate URLs
  given: $.components.schemas.Product.properties
  name: uo-affiliate-tracking-url
  severity: hint
- description: Commission reports should include commission rate
  given: $.components.schemas.CommissionReport.properties
  name: uo-commission-rate-defined
  severity: hint
- description: Seller products must include a SKU
  given: $.components.schemas.SellerProduct.properties
  name: uo-seller-product-sku
  severity: error
- description: Order status should use predefined values
  given: $.components.schemas.Order.properties.status
  name: uo-order-status-enum
  severity: warn
- description: Operations should include Microcks extension for mocking
  given: $.paths[*][get,post,put,patch,delete]
  name: uo-microcks-operation-present
  severity: hint
- description: Responses should include examples for documentation
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: uo-examples-in-responses
  severity: hint
rules_file: rules/urban-outfitters-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/urban-outfitters/refs/heads/main/rules/urban-outfitters-spectral-rules.yml
severity_counts:
  error: 10
  hint: 9
  info: 0
  warn: 12
slug: urban-outfitters-spectral-rules
source_filename: urban-outfitters-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # Info Rules\n  uo-info-title-present:\n    description: API info must have a title\n    message: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  uo-info-description-present:\n    description: API info must have a description\n    message: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  uo-info-version-present:\n    description: API info must have a version\n    message: Info object must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  # OpenAPI Version Rules\n  uo-openapi-version:\n    description: Must use OpenAPI 3.x\n    message: OpenAPI version must be 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # Server Rules\n\
  \  uo-servers-present:\n    description: API must define servers\n    message: Servers array must be defined and non-empty\n    severity: warn\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  uo-server-url-https:\n    description: Server URLs should use HTTPS\n    message: \"Server URL should use HTTPS: {{value}}\"\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Path Rules\n  uo-paths-present:\n    description: API must define paths\n    message: Paths object must be defined and non-empty\n    severity: error\n    given: $\n    then:\n      field: paths\n      function: truthy\n\n  uo-path-lowercase:\n    description: Path segments should be lowercase\n    message: \"Path should use lowercase letters: {{value}}\"\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9/_{}.-]*$\"\n\n  # Operation\
  \ Rules\n  uo-operation-id-present:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  uo-operation-summary-present:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  uo-operation-description-present:\n    description: All operations should have a description\n    message: Operation should have a description\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  uo-operation-tags-present:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n\
  \    then:\n      field: tags\n      function: truthy\n\n  # Tag Rules\n  uo-tags-defined:\n    description: All tags used in operations should be defined at the top level\n    message: Tags should be defined in the global tags array\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  # Parameter Rules\n  uo-parameter-description-present:\n    description: All parameters should have a description\n    message: Parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  uo-parameter-schema-present:\n    description: All parameters must have a schema\n    message: Parameter must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # Request Body Rules\n  uo-request-body-description:\n    description: Request bodies should\
  \ have a description\n    message: Request body should have a description\n    severity: hint\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: description\n      function: truthy\n\n  # Response Rules\n  uo-response-description-present:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  uo-response-success-present:\n    description: Operations must have at least one success (2xx) response\n    message: Operation must define a 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required:\
  \ [\"204\"]\n\n  uo-response-error-present:\n    description: Operations should define error responses\n    message: Operation should define at least one error response (4xx or 5xx)\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"500\"]\n\n  # Schema Rules\n  uo-schema-description-present:\n    description: All schemas should have a description\n    message: Schema should have a description\n    severity: hint\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  uo-schema-properties-examples:\n    description: Schema properties should include examples\n    message: Schema property should have an example value\n    severity: hint\n\
  \    given: $.components.schemas[*].properties[*]\n    then:\n      field: example\n      function: truthy\n\n  # Security Rules\n  uo-security-schemes-defined:\n    description: API must define security schemes\n    message: Security schemes must be defined in components\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  uo-global-security-present:\n    description: API should define global security requirements\n    message: Global security array should be defined\n    severity: warn\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  # HTTP Method Rules\n  uo-get-no-request-body:\n    description: GET operations should not have a request body\n    message: GET operation should not have a request body\n    severity: warn\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  uo-delete-no-body:\n    description: DELETE operations should not have a request body\n\
  \    message: DELETE operation should not have a request body\n    severity: hint\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  # Affiliate-Specific Rules\n  uo-affiliate-tracking-url:\n    description: Affiliate product responses should include affiliate URLs\n    message: Affiliate API product schema should include affiliateUrl field\n    severity: hint\n    given: $.components.schemas.Product.properties\n    then:\n      field: affiliateUrl\n      function: truthy\n\n  uo-commission-rate-defined:\n    description: Commission reports should include commission rate\n    message: CommissionReport schema should define commissionRate\n    severity: hint\n    given: $.components.schemas.CommissionReport.properties\n    then:\n      field: commissionRate\n      function: truthy\n\n  # Marketplace-Specific Rules\n  uo-seller-product-sku:\n    description: Seller products must include a SKU\n    message: SellerProduct schema must include sku field\n\
  \    severity: error\n    given: $.components.schemas.SellerProduct.properties\n    then:\n      field: sku\n      function: truthy\n\n  uo-order-status-enum:\n    description: Order status should use predefined values\n    message: Order status field should define an enum\n    severity: warn\n    given: $.components.schemas.Order.properties.status\n    then:\n      field: enum\n      function: truthy\n\n  # Quality Rules\n  uo-microcks-operation-present:\n    description: Operations should include Microcks extension for mocking\n    message: Operation should have x-microcks-operation extension\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  uo-examples-in-responses:\n    description: Responses should include examples for documentation\n    message: Response content should include examples\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]\n    then:\n\
  \      field: examples\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/urban-outfitters/refs/heads/main/rules/urban-outfitters-spectral-rules.yml
tags:
- Retail
- Fashion
- Apparel
- Ecommerce
- Affiliate
- Marketplace
- Spectral
- Linting
- API Governance
---
