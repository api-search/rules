---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache Samza.
layout: rules
name: Apache Samza API Rules
provider_name: Apache Samza
provider_slug: apache-samza
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-samza-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-samza-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-samza-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-samza-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache Samza
  given: $.paths[*][*].summary
  name: apache-samza-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-samza-response-success-required
  severity: error
rules_file: rules/apache-samza-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-samza/refs/heads/main/rules/apache-samza-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-samza-spectral-rules
tags:
- Big Data
- Hadoop
- Kafka
- Stream Processing
- Streaming
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
