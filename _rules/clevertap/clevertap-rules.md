---
categories:
- clevertap
description: Spectral linting rules defining API design standards and conventions for CleverTap.
layout: rules
name: CleverTap API Rules
provider_name: CleverTap
provider_slug: clevertap
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: clevertap-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clevertap-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clevertap-server-https
  severity: error
- description: A security scheme (apiKey for X-CleverTap-Account-Id and X-CleverTap-Passcode) must be declared.
  given: $.components.securitySchemes
  name: clevertap-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clevertap-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clevertap-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clevertap-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clevertap-error-responses
  severity: warn
rules_file: rules/clevertap-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clevertap/refs/heads/main/rules/clevertap-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: clevertap-rules
tags:
- Audiences
- Customer Engagement
- Customer Retention
- Marketing Automation
- Mobile Engagement
- Push Notifications
- User Behavior
- Spectral
- Linting
- API Governance
---
