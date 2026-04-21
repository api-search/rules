---
categories:
- info
- operation
- paths
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache ORC.
layout: rules
name: Apache ORC API Rules
provider_name: Apache ORC
provider_slug: apache-orc
rule_count: 8
rules:
- description: API must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Operations must have summaries
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-tags-required
  severity: warn
- description: Summaries should start with Apache ORC
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: ''
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: ''
  given: $.paths[*][*].responses
  name: response-success-required
  severity: error
- description: ''
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
rules_file: rules/apache-orc-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-orc/refs/heads/main/rules/apache-orc-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 3
slug: apache-orc-spectral-rules
tags:
- Big Data
- Columnar Storage
- Compression
- File Format
- Hadoop
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
