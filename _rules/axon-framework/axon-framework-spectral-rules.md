---
categories:
- axon
description: Spectral linting rules defining API design standards and conventions for Axon Framework.
layout: rules
name: Axon Framework API Rules
provider_name: Axon Framework
provider_slug: axon-framework
rule_count: 5
rules:
- description: All operations must have a summary starting with "Axon Framework"
  given: $.paths[*][get,post,put,delete,patch]
  name: axon-operation-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: axon-operation-id
  severity: error
- description: Info object must have a title
  given: $.info
  name: axon-info-title
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: axon-response-description
  severity: error
- description: Operations should have x-microcks-operation annotation
  given: $.paths[*][get,post,put,delete,patch]
  name: axon-microcks-annotation
  severity: info
rules_file: rules/axon-framework-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/axon-framework/refs/heads/main/rules/axon-framework-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 1
slug: axon-framework-spectral-rules
tags:
- CQRS
- Event Sourcing
- Event-Driven
- Java
- Messaging
- Microservices
- Spectral
- Linting
- API Governance
---
