---
categories:
- get
- info
- 'no'
- openapi
- operation
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apache JMeter.
layout: rules
name: Apache JMeter API Rules
provider_name: Apache JMeter
provider_slug: apache-jmeter
rule_count: 12
rules:
- description: Info title should start with Apache JMeter
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
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-jmeter-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-jmeter/refs/heads/main/rules/apache-jmeter-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 1
  warn: 2
slug: apache-jmeter-spectral-rules
tags:
- API Testing
- Java
- Load Testing
- Open Source
- Performance Testing
- Stress Testing
- Spectral
- Linting
- API Governance
---
