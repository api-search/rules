---
categories:
- info
- operation
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache Flume.
layout: rules
name: Apache Flume API Rules
provider_name: Apache Flume
provider_slug: apache-flume
rule_count: 7
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
- description: Operation summaries should start with Apache Flume
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-flume-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
rules_file: rules/apache-flume-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-flume/refs/heads/main/rules/apache-flume-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 2
slug: apache-flume-spectral-rules
tags:
- Apache
- Data Collection
- ETL
- Log Aggregation
- Open Source
- Streaming
- Spectral
- Linting
- API Governance
---
