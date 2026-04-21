---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache ShardingSphere.
layout: rules
name: Apache ShardingSphere API Rules
provider_name: Apache ShardingSphere
provider_slug: apache-shardingsphere
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-shardingsphere-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-shardingsphere-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-shardingsphere-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-shardingsphere-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache ShardingSphere
  given: $.paths[*][*].summary
  name: apache-shardingsphere-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-shardingsphere-response-success-required
  severity: error
rules_file: rules/apache-shardingsphere-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-shardingsphere/refs/heads/main/rules/apache-shardingsphere-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-shardingsphere-spectral-rules
tags:
- Database
- Distributed SQL
- Read-Write Splitting
- Sharding
- SQL
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
