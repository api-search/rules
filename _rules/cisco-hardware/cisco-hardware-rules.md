---
categories:
- cisco
description: Spectral linting rules defining API design standards and conventions for Cisco Hardware.
layout: rules
name: Cisco Hardware API Rules
provider_name: Cisco Hardware
provider_slug: cisco-hardware
rule_count: 6
rules:
- description: API info object MUST contain a contact for Cisco Hardware APIs.
  given: $.info
  name: cisco-hardware-info-contact
  severity: warn
- description: All Cisco Hardware API servers MUST use HTTPS.
  given: $.servers[*].url
  name: cisco-hardware-https-only
  severity: error
- description: Operations MUST be tagged for hardware domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: cisco-hardware-tag-required
  severity: warn
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: cisco-hardware-operation-id
  severity: error
- description: Operations MUST have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: cisco-hardware-summary-required
  severity: warn
- description: API MUST define security schemes for token, basic-auth, or signature auth.
  given: $.components.securitySchemes
  name: cisco-hardware-security-required
  severity: error
rules_file: rules/cisco-hardware-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-hardware/refs/heads/main/rules/cisco-hardware-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 3
slug: cisco-hardware-rules
tags:
- Hardware
- Infrastructure
- Networking
- Routers
- Switches
- Spectral
- Linting
- API Governance
---
