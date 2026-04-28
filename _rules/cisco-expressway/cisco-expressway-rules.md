---
categories:
- expressway
description: Spectral linting rules defining API design standards and conventions for Cisco Expressway.
layout: rules
name: Cisco Expressway API Rules
provider_name: Cisco Expressway
provider_slug: cisco-expressway
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: expressway-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: expressway-server-https
  severity: error
- description: Servers must include /api/provisioning or /api/status.
  given: $.servers[*].url
  name: expressway-server-base-path
  severity: warn
- description: A basic-auth security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: expressway-basic-auth
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: expressway-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: expressway-operation-tags
  severity: warn
- description: Provisioning collection paths should be plural nouns.
  given: $.paths[?(@property.indexOf('/api/provisioning/') > -1)]~
  name: expressway-zone-collection-naming
  severity: info
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: expressway-error-responses
  severity: warn
rules_file: rules/cisco-expressway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-expressway/refs/heads/main/rules/cisco-expressway-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 3
slug: cisco-expressway-rules
tags:
- Collaboration
- Firewall Traversal
- H.323
- Session Border Controller
- SIP
- Unified Communications
- Video Conferencing
- Spectral
- Linting
- API Governance
---
