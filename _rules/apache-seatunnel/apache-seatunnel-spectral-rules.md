---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache SeaTunnel.
layout: rules
name: Apache SeaTunnel API Rules
provider_name: Apache SeaTunnel
provider_slug: apache-seatunnel
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-seatunnel-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-seatunnel-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-seatunnel-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-seatunnel-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache SeaTunnel
  given: $.paths[*][*].summary
  name: apache-seatunnel-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-seatunnel-response-success-required
  severity: error
rules_file: rules/apache-seatunnel-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-seatunnel/refs/heads/main/rules/apache-seatunnel-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-seatunnel-spectral-rules
tags:
- Data Integration
- ETL
- ELT
- Batch
- Streaming
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
