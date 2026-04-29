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
source_yaml: "extends:\n  - spectral:oas\nrules:\n  webex-server-https:\n    description: All Webex API servers MUST use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n  webex-base-url:\n    description: Webex server URL SHOULD be webexapis.com/v1.\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://webexapis\\.com/v1'\n  webex-operation-id:\n    description: Operations MUST have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n  webex-summary-required:\n    description: Operations MUST have a summary.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n  webex-tag-required:\n    description: Operations MUST be tagged for Webex domain grouping.\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].tags\n    then:\n      function: truthy\n  webex-oauth-security:\n    description: API SHOULD declare OAuth 2.0 security scheme.\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cisco-webex/refs/heads/main/rules/cisco-webex-rules.yml
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
