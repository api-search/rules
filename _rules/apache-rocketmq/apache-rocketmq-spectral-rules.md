---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache RocketMQ.
layout: rules
name: Apache RocketMQ API Rules
provider_name: Apache RocketMQ
provider_slug: apache-rocketmq
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-rocketmq-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-rocketmq-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-rocketmq-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-rocketmq-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache RocketMQ
  given: $.paths[*][*].summary
  name: apache-rocketmq-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-rocketmq-response-success-required
  severity: error
rules_file: rules/apache-rocketmq-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-rocketmq/refs/heads/main/rules/apache-rocketmq-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-rocketmq-spectral-rules
tags:
- Cloud Native
- Messaging
- Message Queue
- Pub-Sub
- Streaming
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
