---
categories:
- info
- operation
- parameter
- response
- schema
- security
description: Spectral linting rules defining API design standards and conventions for Apache Guacamole.
layout: rules
name: Apache Guacamole API Rules
provider_name: Apache Guacamole
provider_slug: apache-guacamole
rule_count: 10
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
- description: Operation summaries should start with Apache Guacamole
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-guacamole-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: Operations should have tags
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: All session operations require Guacamole-Token header
  given: $.paths./api/session[*][get,post,put,delete].parameters[?(@.name=='Guacamole-Token')]
  name: security-token-required
  severity: warn
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
rules_file: rules/apache-guacamole-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-guacamole/refs/heads/main/rules/apache-guacamole-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: apache-guacamole-spectral-rules
tags:
- Apache
- Open Source
- RDP
- Remote Access
- Remote Desktop
- SSH
- VNC
- Web Gateway
- Spectral
- Linting
- API Governance
---
