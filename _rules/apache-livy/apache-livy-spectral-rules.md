---
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Livy.
layout: rules
name: Apache Livy API Rules
provider_name: Apache Livy
provider_slug: apache-livy
rule_count: 13
rules:
- description: Info title should start with Apache Livy
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
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put].parameters[*]
  name: parameter-description-required
  severity: warn
rules_file: rules/apache-livy-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-livy/refs/heads/main/rules/apache-livy-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 1
  warn: 3
slug: apache-livy-spectral-rules
tags:
- Big Data
- Interactive Computing
- Open Source
- REST
- Spark
- Spectral
- Linting
- API Governance
---
