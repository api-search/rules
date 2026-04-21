---
categories:
- info
- operation
- parameter
- paths
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache Flink.
layout: rules
name: Apache Flink API Rules
provider_name: Apache Flink
provider_slug: apache-flink
rule_count: 11
rules:
- description: Info title must be defined
  given: $.info
  name: info-title-required
  severity: error
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache Flink
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-flink-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: Operations should have tags for grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define at least one 2xx response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
rules_file: rules/apache-flink-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-flink/refs/heads/main/rules/apache-flink-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 5
slug: apache-flink-spectral-rules
tags:
- Apache
- Batch Processing
- Big Data
- Open Source
- Real-Time Analytics
- Stateful Computing
- Stream Processing
- Spectral
- Linting
- API Governance
---
