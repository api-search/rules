---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache Ranger.
layout: rules
name: Apache Ranger API Rules
provider_name: Apache Ranger
provider_slug: apache-ranger
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-ranger-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-ranger-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-ranger-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-ranger-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache Ranger
  given: $.paths[*][*].summary
  name: apache-ranger-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-ranger-response-success-required
  severity: error
rules_file: rules/apache-ranger-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-ranger/refs/heads/main/rules/apache-ranger-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-ranger-spectral-rules
tags:
- Access Control
- Authorization
- Hadoop
- Policy Management
- Security
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
