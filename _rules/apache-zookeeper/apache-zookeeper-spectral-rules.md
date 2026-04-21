---
categories:
- info
- operation
- paths
- response
- servers
description: Spectral linting rules defining API design standards and conventions for Apache ZooKeeper.
layout: rules
name: Apache ZooKeeper API Rules
provider_name: Apache ZooKeeper
provider_slug: apache-zookeeper
rule_count: 10
rules:
- description: Info title is required
  given: $.info
  name: info-title-required
  severity: error
- description: API version is required
  given: $.info
  name: info-version-required
  severity: error
- description: Servers array must be defined
  given: $
  name: servers-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: Operation summaries should start with "Apache ZooKeeper"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: info
- description: Every operation should have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: All operations should have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Path segments should use kebab-case or be simple command names
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
rules_file: rules/apache-zookeeper-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-zookeeper/refs/heads/main/rules/apache-zookeeper-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 2
  warn: 1
slug: apache-zookeeper-spectral-rules
tags:
- Configuration Management
- Distributed Coordination
- Leader Election
- Service Discovery
- Open Source
- Spectral
- Linting
- API Governance
---
