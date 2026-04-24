---
categories:
- bjs
description: Spectral linting rules defining API design standards and conventions for BJ's Wholesale Club.
layout: rules
name: BJ's Wholesale Club API Rules
provider_name: BJ's Wholesale Club
provider_slug: bjs-wholesale-club
rule_count: 5
rules:
- description: Orders and membership verifications must include a membershipNumber
  given: $.paths['/membership/verify'].post.requestBody.content['application/json'].schema
  name: bjs-membership-number-required
  severity: warn
- description: Order status must be one of the defined enum values
  given: $.components.schemas.Order.properties.status
  name: bjs-order-status-enum
  severity: warn
- description: Product price must be defined as a number type
  given: $.components.schemas.Product.properties.price
  name: bjs-product-price-positive
  severity: warn
- description: All endpoints must use ApiKeyAuth security scheme
  given: $.paths[*][*]
  name: bjs-api-key-security
  severity: warn
- description: All operations should have at least one tag
  given: $.paths[*][*]
  name: bjs-operations-have-tags
  severity: warn
rules_file: rules/bjs-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bjs-wholesale-club/refs/heads/main/rules/bjs-spectral-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 5
slug: bjs-spectral-rules
tags:
- Ecommerce
- Membership
- Retail
- Wholesale
- Spectral
- Linting
- API Governance
---
