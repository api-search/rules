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
description: Spectral linting rules defining API design standards and conventions for Apache Kylin.
layout: rules
name: Apache Kylin API Rules
provider_name: Apache Kylin
provider_slug: apache-kylin
rule_count: 12
rules:
- description: Info title should start with Apache Kylin
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
- description: Servers must be defined
  given: $
  name: servers-defined
  severity: error
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
rules_file: rules/apache-kylin-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-kylin/refs/heads/main/rules/apache-kylin-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 0
  warn: 2
slug: apache-kylin-spectral-rules
tags:
- Analytics
- Big Data
- Cube
- OLAP
- Open Source
- SQL
- Spectral
- Linting
- API Governance
---
