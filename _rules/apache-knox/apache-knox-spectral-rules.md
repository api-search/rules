---
categories:
- get
- info
- 'no'
- openapi
- operation
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Knox.
layout: rules
name: Apache Knox API Rules
provider_name: Apache Knox
provider_slug: apache-knox
rule_count: 12
rules:
- description: Info title should start with Apache Knox
  given: $.info
  name: info-title-prefix
  severity: warn
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version
  severity: error
- description: Knox API should use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Responses must have descriptions
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-2xx-required
  severity: error
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: error
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-knox-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-knox/refs/heads/main/rules/apache-knox-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 3
slug: apache-knox-spectral-rules
tags:
- API Gateway
- Authentication
- Hadoop
- Open Source
- Security
- SSO
- Spectral
- Linting
- API Governance
---
