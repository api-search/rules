---
categories:
- info
- operation
- response
- servers
description: Spectral linting rules defining API design standards and conventions for APIGit.
layout: rules
name: APIGit API Rules
provider_name: APIGit
provider_slug: apigit
rule_count: 6
rules:
- description: API title must start with 'APIGit'.
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
- description: Operation summaries must start with 'APIGit'.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
rules_file: rules/apigit-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apigit/refs/heads/main/rules/apigit-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apigit-spectral-rules
tags:
- API Design
- API Lifecycle
- Documentation
- Git
- Governance
- Mocking
- Platform
- Testing
- Spectral
- Linting
- API Governance
---
