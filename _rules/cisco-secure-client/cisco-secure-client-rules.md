---
categories:
- csc
description: Spectral linting rules defining API design standards and conventions for Cisco Secure Client.
layout: rules
name: Cisco Secure Client API Rules
provider_name: Cisco Secure Client
provider_slug: cisco-secure-client
rule_count: 5
rules:
- description: All Secure Client management API servers MUST use HTTPS.
  given: $.servers[*].url
  name: csc-https-only
  severity: error
- description: API MUST define security schemes for token, OAuth, or HMAC auth.
  given: $.components.securitySchemes
  name: csc-security-required
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: csc-operation-id
  severity: error
- description: Operations MUST be tagged for security domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: csc-tag-required
  severity: warn
- description: API info MUST contain a contact for security disclosures.
  given: $.info
  name: csc-info-contact
  severity: warn
rules_file: rules/cisco-secure-client-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-secure-client/refs/heads/main/rules/cisco-secure-client-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 2
slug: cisco-secure-client-rules
tags:
- Endpoint Security
- Remote Access
- Security
- VPN
- Zero Trust
- Spectral
- Linting
- API Governance
---
