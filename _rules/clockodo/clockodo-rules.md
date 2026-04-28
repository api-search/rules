---
categories:
- clockodo
description: Spectral linting rules defining API design standards and conventions for Clockodo.
layout: rules
name: Clockodo API Rules
provider_name: Clockodo
provider_slug: clockodo
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: clockodo-info-contact
  severity: warn
- description: All Clockodo API servers MUST use HTTPS.
  given: $.servers[*].url
  name: clockodo-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: clockodo-operation-id
  severity: error
- description: Operations MUST be tagged for resource grouping (Entries, Customers, Projects, Services, Users, Absences, LumpSumServices, HolidaysQuota, Clock).
  given: $.paths[*][get,post,put,delete,patch].tags
  name: clockodo-tag-required
  severity: warn
- description: API MUST define API-key and/or basic-auth security since Clockodo authenticates with X-ClockodoApiUser/X-ClockodoApiKey headers or HTTP Basic.
  given: $.components.securitySchemes
  name: clockodo-auth-required
  severity: error
- description: API MUST declare at least one server URL pointing at my.clockodo.com.
  given: $.servers
  name: clockodo-server-url
  severity: error
rules_file: rules/clockodo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clockodo/refs/heads/main/rules/clockodo-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: clockodo-rules
tags:
- Absence Management
- Billing
- Project Management
- Stop Clock
- Time Tracking
- Timesheets
- Spectral
- Linting
- API Governance
---
