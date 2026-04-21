---
categories:
- examples
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Ignite.
layout: rules
name: Apache Ignite API Rules
provider_name: Apache Ignite
provider_slug: apache-ignite
rule_count: 23
rules:
- description: Info title must be present and start with Apache Ignite
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Info must have a version field
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
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache Ignite
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-prefix
  severity: warn
- description: Every operation should have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Security schemes should be defined
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: POST/PUT operations should document 400 responses
  given: $.paths[*][post,put].responses
  name: response-error-400
  severity: info
- description: GET operations should document 404 responses
  given: $.paths[*].get.responses
  name: response-error-404
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/apache-ignite-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-ignite/refs/heads/main/rules/apache-ignite-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 4
  warn: 9
slug: apache-ignite-spectral-rules
tags:
- Caching
- Compute Grid
- Distributed Database
- In-Memory
- Open Source
- SQL
- Spectral
- Linting
- API Governance
---
