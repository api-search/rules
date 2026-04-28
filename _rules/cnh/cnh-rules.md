---
categories:
- cnh
description: Spectral linting rules defining API design standards and conventions for CNH.
layout: rules
name: CNH API Rules
provider_name: CNH
provider_slug: cnh
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cnh-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cnh-server-https
  severity: error
- description: Production server should target api.fieldops.cnh.com or api.cnh.com.
  given: $.servers[*].url
  name: cnh-server-host
  severity: warn
- description: An OAuth 2.0 security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: cnh-oauth-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cnh-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cnh-operation-tags
  severity: warn
- description: Telemetry GET operations must accept startDate and endDate query parameters (one-day window recommended).
  given: $.paths[?(@property && @property.indexOf('/telemetry') > -1 || @property.indexOf('/metrics') > -1)].get
  name: cnh-telemetry-date-range
  severity: warn
- description: Telemetry endpoints should expose a `profile` parameter restricted to CP or MH.
  given: $.paths[?(@property && @property.indexOf('/telemetry') > -1)].get.parameters[?(@.name == 'profile')].schema
  name: cnh-iso15143-profile
  severity: info
- description: Operations should declare 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: cnh-error-401
  severity: warn
rules_file: rules/cnh-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cnh/refs/heads/main/rules/cnh-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 4
slug: cnh-rules
tags:
- Agriculture
- Construction
- Telematics
- Equipment
- FieldOps
- Spectral
- Linting
- API Governance
---
