---
categories:
- adp
description: Spectral linting rules defining API design standards and conventions for Architectural Design Patterns.
layout: rules
name: Architectural Design Patterns API Rules
provider_name: Architectural Design Patterns
provider_slug: architectural-design-patterns
rule_count: 12
rules:
- description: Pattern must have an id field
  given: $.components.schemas.Pattern.properties
  name: adp-pattern-id-required
  severity: error
- description: Pattern must have a name field
  given: $.components.schemas.Pattern.properties
  name: adp-pattern-name-required
  severity: error
- description: Pattern must have a description field
  given: $.components.schemas.Pattern.properties
  name: adp-pattern-description-required
  severity: error
- description: Relationship type must be a valid enum value
  given: $.components.schemas.Relationship.properties.relationshipType
  name: adp-relationship-type-enum
  severity: error
- description: Pattern category must be a valid enum value
  given: $.paths./patterns.get.parameters[?(@.name=='category')].schema
  name: adp-category-enum
  severity: warn
- description: All API operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: adp-operations-have-tags
  severity: warn
- description: All API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: adp-operations-have-summary
  severity: error
- description: All API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: adp-operations-have-operation-id
  severity: error
- description: List responses must include a total count
  given: $.components.schemas[*List].properties
  name: adp-list-responses-have-total
  severity: warn
- description: Anti-pattern must have a name field
  given: $.components.schemas.AntiPattern.properties
  name: adp-anti-pattern-name-required
  severity: error
- description: API info must include contact information
  given: $.info
  name: adp-info-contact-required
  severity: warn
- description: API must define at least one server
  given: $
  name: adp-servers-defined
  severity: error
rules_file: rules/architectural-design-patterns-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/architectural-design-patterns/refs/heads/main/rules/architectural-design-patterns-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 4
slug: architectural-design-patterns-spectral-rules
tags:
- Design Patterns
- Software Architecture
- Best Practices
- Software Engineering
- System Design
- Microservices
- Spectral
- Linting
- API Governance
---
