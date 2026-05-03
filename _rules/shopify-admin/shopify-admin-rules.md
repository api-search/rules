---
api_specs:
- filename: shopify-admin-rest-openapi.yml
  format: yaml
  label: Shopify Admin REST API
  slug: shopify-admin-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify-admin/refs/heads/main/openapi/shopify-admin-rest-openapi.yml
categories:
- shopify
description: Spectral linting rules defining API design standards and conventions for Shopify Admin API.
layout: rules
name: Shopify Admin API API Rules
provider_name: Shopify Admin API
provider_slug: shopify-admin
rule_count: 9
rules:
- description: Shopify Admin REST API paths must include the API version in the server URL, not the path
  given: $.paths[*]~
  name: shopify-admin-path-version
  severity: warn
- description: Shopify Admin REST API paths typically end with .json
  given: $.paths[*]~
  name: shopify-admin-json-suffix
  severity: info
- description: Shopify Admin REST API resource names should use plural snake_case
  given: $.paths[*]~
  name: shopify-admin-resource-naming
  severity: warn
- description: Shopify Admin REST API requires X-Shopify-Access-Token authentication
  given: $.components.securitySchemes
  name: shopify-admin-access-token-required
  severity: error
- description: All Shopify Admin API operations must have unique operationIds
  given: $.paths[*][get,post,put,delete,patch]
  name: shopify-admin-operation-ids
  severity: error
- description: GET operations must have a 200 response defined
  given: $.paths[*].get
  name: shopify-admin-response-200
  severity: error
- description: All operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: shopify-admin-tag-defined
  severity: warn
- description: Path parameters should use snake_case naming (e.g., product_id, customer_id)
  given: $.paths[*].parameters[?(@.in == 'path')].name
  name: shopify-admin-path-parameter-names
  severity: warn
- description: Shopify Admin API paths must not have trailing slashes
  given: $.paths[*]~
  name: shopify-admin-no-trailing-slash
  severity: warn
rules_file: rules/shopify-admin-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shopify-admin/refs/heads/main/rules/shopify-admin-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: shopify-admin-rules
source_filename: shopify-admin-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shopify-admin-path-version:\n    description: Shopify Admin REST API paths must include the API version in the server URL, not the path\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/admin/api/\"\n\n  shopify-admin-json-suffix:\n    description: Shopify Admin REST API paths typically end with .json\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\.(json)$|\\\\{[a-z_]+\\\\}\"\n\n  shopify-admin-resource-naming:\n    description: Shopify Admin REST API resource names should use plural snake_case\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z][a-z0-9_]*s(\\\\.json|/|$)\"\n\n  shopify-admin-access-token-required:\n    description: Shopify Admin REST API requires X-Shopify-Access-Token authentication\n\
  \    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - AccessToken\n\n  shopify-admin-operation-ids:\n    description: All Shopify Admin API operations must have unique operationIds\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  shopify-admin-response-200:\n    description: GET operations must have a 200 response defined\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  shopify-admin-tag-defined:\n    description: All operations must have at least one tag for grouping\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  shopify-admin-path-parameter-names:\n    description: Path parameters should use snake_case\
  \ naming (e.g., product_id, customer_id)\n    severity: warn\n    given: \"$.paths[*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  shopify-admin-no-trailing-slash:\n    description: Shopify Admin API paths must not have trailing slashes\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shopify-admin/refs/heads/main/rules/shopify-admin-rules.yml
tags:
- Commerce
- Ecommerce
- Admin
- Products
- Orders
- Customers
- Spectral
- Linting
- API Governance
---
