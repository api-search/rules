---
categories:
- get
- info
- operation
- parameter
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Atlas.
layout: rules
name: Apache Atlas API Rules
provider_name: Apache Atlas
provider_slug: apache-atlas
rule_count: 12
rules:
- description: API title must start with "Apache Atlas"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: ''
  given: $.info
  name: info-description-required
  severity: error
- description: ''
  given: $
  name: servers-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-apache-atlas
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: ''
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: ''
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
rules_file: rules/apache-atlas-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-atlas/refs/heads/main/rules/apache-atlas-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 5
slug: apache-atlas-spectral-rules
tags:
- Apache
- Big Data
- Compliance
- Data Governance
- Data Lineage
- Hadoop
- Metadata
- Open Source
- Spectral
- Linting
- API Governance
---
