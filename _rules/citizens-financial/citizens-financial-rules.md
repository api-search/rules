---
categories:
- citizens
description: Spectral linting rules defining API design standards and conventions for Citizens Financial.
layout: rules
name: Citizens Financial API Rules
provider_name: Citizens Financial
provider_slug: citizens-financial
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: citizens-info-contact
  severity: warn
- description: All Citizens Financial API servers MUST use HTTPS.
  given: $.servers[*].url
  name: citizens-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: citizens-operation-id
  severity: error
- description: Operations MUST be tagged for product domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: citizens-tag-required
  severity: warn
- description: API MUST define OAuth 2.0 or other security schemes.
  given: $.components.securitySchemes
  name: citizens-security-required
  severity: error
- description: API MUST declare at least one server URL.
  given: $.servers
  name: citizens-server-url
  severity: error
rules_file: rules/citizens-financial-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/citizens-financial/refs/heads/main/rules/citizens-financial-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: citizens-financial-rules
tags:
- Accounts
- ATMs
- Banking
- Open Banking
- Payments
- Point of Sale
- Transactions
- Spectral
- Linting
- API Governance
---
