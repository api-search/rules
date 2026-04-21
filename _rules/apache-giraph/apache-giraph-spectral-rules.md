---
categories:
- info
- operation
- parameter
- response
description: Spectral linting rules defining API design standards and conventions for Apache Giraph.
layout: rules
name: Apache Giraph API Rules
provider_name: Apache Giraph
provider_slug: apache-giraph
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
- description: Operation summaries should start with Apache Giraph
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-giraph-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
rules_file: rules/apache-giraph-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-giraph/refs/heads/main/rules/apache-giraph-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 3
slug: apache-giraph-spectral-rules
tags:
- Apache
- Big Data
- BSP
- Graph Processing
- Hadoop
- Open Source
- Retired
- Spectral
- Linting
- API Governance
---
