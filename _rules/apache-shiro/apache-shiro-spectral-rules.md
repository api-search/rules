---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache Shiro.
layout: rules
name: Apache Shiro API Rules
provider_name: Apache Shiro
provider_slug: apache-shiro
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-shiro-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-shiro-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-shiro-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-shiro-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache Shiro
  given: $.paths[*][*].summary
  name: apache-shiro-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-shiro-response-success-required
  severity: error
rules_file: rules/apache-shiro-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-shiro/refs/heads/main/rules/apache-shiro-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-shiro-spectral-rules
tags:
- Authentication
- Authorization
- Cryptography
- Java
- Security
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
