---
categories:
- ap
description: Spectral linting rules defining API design standards and conventions for Architecture Pattern.
layout: rules
name: Architecture Pattern API Rules
provider_name: Architecture Pattern
provider_slug: architecture-pattern
rule_count: 12
rules:
- description: Pattern must have an id field
  given: $.components.schemas.Pattern.properties
  name: ap-pattern-id-required
  severity: error
- description: Pattern must have a name field
  given: $.components.schemas.Pattern.properties
  name: ap-pattern-name-required
  severity: error
- description: Pattern must have a problem statement
  given: $.components.schemas.Pattern.properties
  name: ap-pattern-problem-required
  severity: warn
- description: Pattern must have a solution description
  given: $.components.schemas.Pattern.properties
  name: ap-pattern-solution-required
  severity: warn
- description: Pattern confidence must be a valid enum value
  given: $.components.schemas.Pattern.properties.confidence
  name: ap-pattern-confidence-enum
  severity: error
- description: Tradeoff severity must be a valid enum value
  given: $.components.schemas.Tradeoff.properties.severity
  name: ap-tradeoff-severity-enum
  severity: error
- description: List responses must include a total count
  given: $.components.schemas[*List].properties
  name: ap-list-responses-have-total
  severity: warn
- description: All API operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: ap-operations-have-tags
  severity: warn
- description: All API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: ap-operations-have-summary
  severity: error
- description: All API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: ap-operations-have-operation-id
  severity: error
- description: API info must include contact information
  given: $.info
  name: ap-info-contact-required
  severity: warn
- description: API must define at least one server
  given: $
  name: ap-servers-defined
  severity: error
rules_file: rules/architecture-pattern-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/architecture-pattern/refs/heads/main/rules/architecture-pattern-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 5
slug: architecture-pattern-spectral-rules
tags:
- Architecture Patterns
- Software Architecture
- Design Patterns
- System Design
- Microservices
- Cloud Native
- Spectral
- Linting
- API Governance
---
