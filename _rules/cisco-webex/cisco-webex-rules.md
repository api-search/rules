---
categories:
- webex
description: Spectral linting rules defining API design standards and conventions for Cisco Webex.
layout: rules
name: Cisco Webex API Rules
provider_name: Cisco Webex
provider_slug: cisco-webex
rule_count: 6
rules:
- description: All Webex API servers MUST use HTTPS.
  given: $.servers[*].url
  name: webex-server-https
  severity: error
- description: Webex server URL SHOULD be webexapis.com/v1.
  given: $.servers[*].url
  name: webex-base-url
  severity: warn
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: webex-operation-id
  severity: error
- description: Operations MUST have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: webex-summary-required
  severity: warn
- description: Operations MUST be tagged for Webex domain grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: webex-tag-required
  severity: warn
- description: API SHOULD declare OAuth 2.0 security scheme.
  given: $.components.securitySchemes
  name: webex-oauth-security
  severity: warn
rules_file: rules/cisco-webex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-webex/refs/heads/main/rules/cisco-webex-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 4
slug: cisco-webex-rules
tags:
- Collaboration
- Communications
- Meetings
- Messaging
- Teams
- Video Conferencing
- Spectral
- Linting
- API Governance
---
