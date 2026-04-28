---
categories:
- citrix
description: Spectral linting rules defining API design standards and conventions for Citrix.
layout: rules
name: Citrix API Rules
provider_name: Citrix
provider_slug: citrix
rule_count: 7
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: citrix-info-contact
  severity: warn
- description: All Citrix API servers MUST use HTTPS.
  given: $.servers[*].url
  name: citrix-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: citrix-operation-id
  severity: error
- description: Operations MUST be tagged for product domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: citrix-tag-required
  severity: warn
- description: API MUST define security schemes (OAuth 2.0 bearer for Citrix Cloud).
  given: $.components.securitySchemes
  name: citrix-security-required
  severity: error
- description: API MUST declare at least one server URL.
  given: $.servers
  name: citrix-server-url
  severity: error
- description: Customer-scoped Citrix Cloud paths SHOULD use templated customerId.
  given: $.paths
  name: citrix-customer-id-templating
  severity: warn
rules_file: rules/citrix-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/citrix/refs/heads/main/rules/citrix-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 3
slug: citrix-rules
tags:
- Application Delivery
- Desktop-As-A-Service
- Networking
- Virtualization
- Workspace
- Spectral
- Linting
- API Governance
---
