---
categories:
- info
- operation
- response
description: Spectral linting rules defining API design standards and conventions for Apache Pig.
layout: rules
name: Apache Pig API Rules
provider_name: Apache Pig
provider_slug: apache-pig
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
rules_file: rules/apache-pig-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-pig/refs/heads/main/rules/apache-pig-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 0
slug: apache-pig-spectral-rules
tags:
- Big Data
- Data Analysis
- ETL
- Hadoop
- Scripting
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
