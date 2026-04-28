---
categories:
- cisco
description: Spectral linting rules defining API design standards and conventions for Cisco Systems.
layout: rules
name: Cisco Systems API Rules
provider_name: Cisco Systems
provider_slug: cisco-systems
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: cisco-info-contact
  severity: warn
- description: All Cisco Systems API servers MUST use HTTPS.
  given: $.servers[*].url
  name: cisco-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: cisco-operation-id
  severity: error
- description: Operations MUST be tagged for product domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: cisco-tag-required
  severity: warn
- description: API MUST define security schemes.
  given: $.components.securitySchemes
  name: cisco-security-required
  severity: error
- description: API MUST declare at least one server URL.
  given: $.servers
  name: cisco-server-url
  severity: error
rules_file: rules/cisco-systems-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-systems/refs/heads/main/rules/cisco-systems-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: cisco-systems-rules
tags:
- Collaboration
- Infrastructure
- Networking
- Security
- Spectral
- Linting
- API Governance
---
