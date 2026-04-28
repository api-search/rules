---
categories:
- cleanshelf
description: Spectral linting rules defining API design standards and conventions for Cleanshelf.
layout: rules
name: Cleanshelf API Rules
provider_name: Cleanshelf
provider_slug: cleanshelf
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: cleanshelf-info-contact
  severity: warn
- description: All Zylo (Cleanshelf successor) API servers MUST use HTTPS.
  given: $.servers[*].url
  name: cleanshelf-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: cleanshelf-operation-id
  severity: error
- description: Operations MUST be tagged for SaaS-management domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: cleanshelf-tag-required
  severity: warn
- description: API MUST define API key or bearer token security schemes.
  given: $.components.securitySchemes
  name: cleanshelf-security-required
  severity: error
- description: API MUST declare at least one server URL.
  given: $.servers
  name: cleanshelf-server-url
  severity: error
rules_file: rules/cleanshelf-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cleanshelf/refs/heads/main/rules/cleanshelf-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: cleanshelf-rules
tags:
- Acquired
- License Management
- SaaS Management
- Shadow IT
- SMP
- Software Asset Management
- Spend Optimization
- Spectral
- Linting
- API Governance
---
