---
categories:
- info
- operation
- response
- servers
description: Spectral linting rules defining API design standards and conventions for APIGen.
layout: rules
name: APIGen API Rules
provider_name: APIGen
provider_slug: apigen
rule_count: 7
rules:
- description: API title must start with 'APIGen'.
  given: $.info
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Operation summaries must start with 'APIGen'.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have tags.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
rules_file: rules/apigen-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apigen/refs/heads/main/rules/apigen-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 3
slug: apigen-spectral-rules
tags:
- Code
- Documentation
- Generation
- Open Source
- PHP
- Spectral
- Linting
- API Governance
---
