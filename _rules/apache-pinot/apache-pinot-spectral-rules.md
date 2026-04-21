---
categories:
- info
- operation
- response
description: Spectral linting rules defining API design standards and conventions for Apache Pinot.
layout: rules
name: Apache Pinot API Rules
provider_name: Apache Pinot
provider_slug: apache-pinot
rule_count: 5
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: ''
  given: $.paths[*][get,post,put].responses
  name: response-success-required
  severity: error
rules_file: rules/apache-pinot-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-pinot/refs/heads/main/rules/apache-pinot-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 0
slug: apache-pinot-spectral-rules
tags:
- Analytics
- Database
- Low Latency
- OLAP
- Real-Time
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
