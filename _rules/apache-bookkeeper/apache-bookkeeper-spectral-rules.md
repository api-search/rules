---
categories:
- bookkeeper
description: Spectral linting rules defining API design standards and conventions for Apache BookKeeper.
layout: rules
name: Apache BookKeeper API Rules
provider_name: Apache BookKeeper
provider_slug: apache-bookkeeper
rule_count: 12
rules:
- description: API info must have a title
  given: $.info
  name: bookkeeper-admin-info-title
  severity: error
- description: API info must have a description
  given: $.info
  name: bookkeeper-admin-info-description
  severity: warn
- description: API info must have a version
  given: $.info
  name: bookkeeper-admin-info-version
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: bookkeeper-admin-operation-id
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: bookkeeper-admin-operation-summary
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: bookkeeper-admin-operation-tags
  severity: warn
- description: GET and PUT operations should have a 200 response
  given: $.paths[*][get,put]
  name: bookkeeper-admin-response-200
  severity: warn
- description: All component schemas must have a title
  given: $.components.schemas[*]
  name: bookkeeper-admin-schema-title
  severity: warn
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: bookkeeper-admin-schema-description
  severity: warn
- description: Operation summaries should start with Apache BookKeeper
  given: $.paths[*][get,put,post,delete,patch].summary
  name: bookkeeper-admin-summary-prefix
  severity: warn
- description: API paths should use lowercase letters
  given: $.paths
  name: bookkeeper-admin-path-lowercase
  severity: warn
- description: All operations should have x-microcks-operation extension
  given: $.paths[*][get,put,post,delete,patch]
  name: bookkeeper-admin-microcks-operation
  severity: info
rules_file: rules/apache-bookkeeper-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-bookkeeper/refs/heads/main/rules/apache-bookkeeper-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 8
slug: apache-bookkeeper-spectral-rules
tags:
- Apache
- Distributed Systems
- Log Storage
- Open Source
- Storage
- Streaming
- Spectral
- Linting
- API Governance
---
