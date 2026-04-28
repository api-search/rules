---
categories:
- webex
description: Spectral linting rules defining API design standards and conventions for Cisco Control Hub.
layout: rules
name: Cisco Control Hub API Rules
provider_name: Cisco Control Hub
provider_slug: cisco-control-hub
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: webex-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: webex-server-https
  severity: error
- description: webexapis.com servers must include /v1.
  given: $.servers[?(@.url && @.url.indexOf('webexapis.com') > -1)].url
  name: webex-server-base-path
  severity: warn
- description: An OAuth 2.0 security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: webex-oauth-security
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: webex-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: webex-operation-tags
  severity: warn
- description: List endpoints should support max/cursor or start pagination.
  given: $.paths[*].get.parameters[*].name
  name: webex-pagination-cursor
  severity: info
- description: Mutating operations should declare 4xx/5xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: webex-error-responses
  severity: warn
rules_file: rules/cisco-control-hub-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cisco-control-hub/refs/heads/main/rules/cisco-control-hub-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: cisco-control-hub-rules
tags:
- Administration
- Calling
- Collaboration
- Communications
- Device Management
- Identity Management
- Licenses
- Reporting
- Webex
- Spectral
- Linting
- API Governance
---
