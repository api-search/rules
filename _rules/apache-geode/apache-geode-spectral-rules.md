---
categories:
- info
- operation
- parameter
- paths
- response
description: Spectral linting rules defining API design standards and conventions for Apache Geode.
layout: rules
name: Apache Geode API Rules
provider_name: Apache Geode
provider_slug: apache-geode
rule_count: 9
rules:
- description: Info title must be defined
  given: $.info
  name: info-title-required
  severity: error
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache Geode
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-geode-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: Operations should have tags
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Paths should include API version prefix
  given: $.paths
  name: paths-versioned
  severity: info
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
rules_file: rules/apache-geode-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-geode/refs/heads/main/rules/apache-geode-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 4
slug: apache-geode-spectral-rules
tags:
- Apache
- Caching
- Data Grid
- Distributed Systems
- In-Memory
- Open Source
- Spectral
- Linting
- API Governance
---
