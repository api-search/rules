---
categories:
- bigcommerce
description: Spectral linting rules defining API design standards and conventions for BigCommerce.
layout: rules
name: BigCommerce API Rules
provider_name: BigCommerce
provider_slug: bigcommerce
rule_count: 24
rules:
- description: API title must start with "BigCommerce"
  given: $.info.title
  name: bigcommerce-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: bigcommerce-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: bigcommerce-info-contact-present
  severity: warn
- description: API info must have a description
  given: $.info
  name: bigcommerce-info-description-present
  severity: warn
- description: Operation summaries must start with "BigCommerce"
  given: $.paths[*][*].summary
  name: bigcommerce-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: bigcommerce-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: bigcommerce-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: bigcommerce-operation-description-present
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: bigcommerce-path-kebab-case
  severity: warn
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: bigcommerce-response-200-present
  severity: error
- description: Operations must define error responses
  given: $.paths[*][post,put,patch,delete].responses
  name: bigcommerce-response-error-present
  severity: warn
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: bigcommerce-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: bigcommerce-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: bigcommerce-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: bigcommerce-security-scheme-present
  severity: error
- description: Mutating operations must declare security
  given: $.paths[*][post,put,patch,delete]
  name: bigcommerce-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: bigcommerce-tags-defined
  severity: warn
- description: Top-level tags must have a description
  given: $.tags[*]
  name: bigcommerce-tag-description-present
  severity: warn
- description: API must define servers
  given: $
  name: bigcommerce-servers-present
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: bigcommerce-server-url-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: bigcommerce-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: bigcommerce-microcks-operation-present
  severity: warn
- description: Server URLs should use store hash variable
  given: $.servers[*].url
  name: bigcommerce-store-hash-variable
  severity: warn
- description: API info must include license
  given: $.info
  name: bigcommerce-license-present
  severity: warn
rules_file: rules/bigcommerce-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bigcommerce/refs/heads/main/rules/bigcommerce-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 17
slug: bigcommerce-spectral-rules
tags:
- E-Commerce
- Retail
- Catalog
- Orders
- Checkout
- Payments
- SaaS
- Spectral
- Linting
- API Governance
---
