---
categories:
- webex
description: Spectral linting rules defining API design standards and conventions for Cisco Webex Meetings.
layout: rules
name: Cisco Webex Meetings API Rules
provider_name: Cisco Webex Meetings
provider_slug: cisco-webex-meetings
rule_count: 5
rules:
- description: All Webex Meetings API servers MUST use HTTPS.
  given: $.servers[*].url
  name: webex-meetings-server-https
  severity: error
- description: Webex Meetings server URL SHOULD be webexapis.com/v1.
  given: $.servers[*].url
  name: webex-meetings-base-url
  severity: warn
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: webex-meetings-operation-id
  severity: error
- description: Operations MUST be tagged.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: webex-meetings-tag-required
  severity: warn
- description: API SHOULD declare OAuth 2.0 security scheme.
  given: $.components.securitySchemes
  name: webex-meetings-oauth-required
  severity: warn
rules_file: rules/cisco-webex-meetings-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-webex-meetings/refs/heads/main/rules/cisco-webex-meetings-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 3
slug: cisco-webex-meetings-rules
tags:
- Collaboration
- Communications
- Enterprise
- Meetings
- Video Conferencing
- Spectral
- Linting
- API Governance
---
