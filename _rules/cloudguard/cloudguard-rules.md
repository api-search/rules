---
categories:
- cloudguard
description: Spectral linting rules defining API design standards and conventions for CloudGuard.
layout: rules
name: CloudGuard API Rules
provider_name: CloudGuard
provider_slug: cloudguard
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudguard-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudguard-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudguard-server-https
  severity: error
- description: CloudGuard control-plane paths must be versioned (/v{N}/).
  given: $.paths
  name: cloudguard-server-versioned
  severity: warn
- description: A security scheme must be declared (CloudGuard uses HTTP Basic with API key + secret).
  given: $.components.securitySchemes
  name: cloudguard-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudguard-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudguard-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudguard-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudguard-error-responses
  severity: warn
rules_file: rules/cloudguard-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudguard/refs/heads/main/rules/cloudguard-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: cloudguard-rules
tags:
- Check Point
- CNAPP
- Cloud Security
- Compliance
- CSPM
- CWPP
- Posture Management
- Spectral
- Linting
- API Governance
---
