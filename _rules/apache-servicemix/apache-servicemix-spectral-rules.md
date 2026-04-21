---
categories:
- apache
description: Spectral linting rules defining API design standards and conventions for Apache ServiceMix.
layout: rules
name: Apache ServiceMix API Rules
provider_name: Apache ServiceMix
provider_slug: apache-servicemix
rule_count: 6
rules:
- description: Info object must have a title
  given: $.info
  name: apache-servicemix-info-title-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: apache-servicemix-operation-summary-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: apache-servicemix-operation-operationId-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: apache-servicemix-operation-tags-required
  severity: warn
- description: Operation summaries should be prefixed with Apache ServiceMix
  given: $.paths[*][*].summary
  name: apache-servicemix-operation-summary-apache-prefix
  severity: warn
- description: All operations must have a success response
  given: $.paths[*][*].responses
  name: apache-servicemix-response-success-required
  severity: error
rules_file: rules/apache-servicemix-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-servicemix/refs/heads/main/rules/apache-servicemix-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: apache-servicemix-spectral-rules
tags:
- Enterprise Integration
- ESB
- Integration
- Messaging
- OSGi
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
