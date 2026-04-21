---
categories:
- cloudstack
description: Spectral linting rules defining API design standards and conventions for Apache CloudStack.
layout: rules
name: Apache CloudStack API Rules
provider_name: Apache CloudStack
provider_slug: apache-cloudstack
rule_count: 12
rules:
- description: API info must have a title
  given: $.info
  name: cloudstack-api-info-title
  severity: error
- description: API info must have a description
  given: $.info
  name: cloudstack-api-info-description
  severity: warn
- description: API info must have a version
  given: $.info
  name: cloudstack-api-info-version
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: cloudstack-api-operation-id
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: cloudstack-api-operation-summary
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: cloudstack-api-operation-tags
  severity: warn
- description: GET operations should have a 200 response
  given: $.paths[*][get]
  name: cloudstack-api-response-200
  severity: warn
- description: All component schemas must have a title
  given: $.components.schemas[*]
  name: cloudstack-api-schema-title
  severity: warn
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: cloudstack-api-schema-description
  severity: warn
- description: Operation summaries should start with Apache CloudStack
  given: $.paths[*][get,put,post,delete,patch].summary
  name: cloudstack-api-summary-prefix
  severity: warn
- description: All operations should use apiKeyAuth security
  given: $.paths[*][get,put,post,delete,patch]
  name: cloudstack-api-apikey-security
  severity: warn
- description: All operations should have x-microcks-operation extension
  given: $.paths[*][get,put,post,delete,patch]
  name: cloudstack-api-microcks-operation
  severity: info
rules_file: rules/apache-cloudstack-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-cloudstack/refs/heads/main/rules/apache-cloudstack-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 8
slug: apache-cloudstack-spectral-rules
tags:
- Apache
- Cloud
- IaaS
- Infrastructure
- Open Source
- Virtualization
- Spectral
- Linting
- API Governance
---
