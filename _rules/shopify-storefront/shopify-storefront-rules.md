---
api_specs:
- filename: shopify-storefront-openapi.yml
  format: yaml
  label: Shopify Storefront API
  slug: shopify-storefront-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify-storefront/refs/heads/main/openapi/shopify-storefront-openapi.yml
categories:
- shopify
description: Spectral linting rules defining API design standards and conventions for Shopify Storefront API.
layout: rules
name: Shopify Storefront API API Rules
provider_name: Shopify Storefront API
provider_slug: shopify-storefront
rule_count: 6
rules:
- description: Shopify Storefront API uses a single GraphQL endpoint
  given: $.paths
  name: shopify-storefront-graphql-endpoint
  severity: info
- description: Storefront API requires X-Shopify-Storefront-Access-Token authentication
  given: $.components.securitySchemes
  name: shopify-storefront-access-token
  severity: error
- description: All Storefront API operations must have operationIds
  given: $.paths[*][get,post,put,delete,patch]
  name: shopify-storefront-operation-id
  severity: error
- description: GraphQL endpoint should accept application/json content type
  given: $.paths[*].post.requestBody.content
  name: shopify-storefront-graphql-content-type
  severity: warn
- description: GraphQL responses should have data and errors fields
  given: $.components.schemas.GraphQLResponse.properties
  name: shopify-storefront-graphql-response
  severity: warn
- description: Shopify Storefront API uses global IDs in gid://shopify/ format
  given: $.components.schemas.*.properties.id
  name: shopify-storefront-gid-format
  severity: info
rules_file: rules/shopify-storefront-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shopify-storefront/refs/heads/main/rules/shopify-storefront-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 2
slug: shopify-storefront-rules
source_filename: shopify-storefront-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shopify-storefront-graphql-endpoint:\n    description: Shopify Storefront API uses a single GraphQL endpoint\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          maxProperties: 2\n\n  shopify-storefront-access-token:\n    description: Storefront API requires X-Shopify-Storefront-Access-Token authentication\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - StorefrontAccessToken\n\n  shopify-storefront-operation-id:\n    description: All Storefront API operations must have operationIds\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  shopify-storefront-graphql-content-type:\n    description: GraphQL endpoint\
  \ should accept application/json content type\n    severity: warn\n    given: \"$.paths[*].post.requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - application/json\n\n  shopify-storefront-graphql-response:\n    description: GraphQL responses should have data and errors fields\n    severity: warn\n    given: \"$.components.schemas.GraphQLResponse.properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - data\n            - errors\n\n  shopify-storefront-gid-format:\n    description: Shopify Storefront API uses global IDs in gid://shopify/ format\n    severity: info\n    given: \"$.components.schemas.*.properties.id\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            description:\n              type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shopify-storefront/refs/heads/main/rules/shopify-storefront-rules.yml
tags:
- Commerce
- Ecommerce
- Headless
- GraphQL
- Storefront
- Products
- Cart
- Checkout
- Spectral
- Linting
- API Governance
---
