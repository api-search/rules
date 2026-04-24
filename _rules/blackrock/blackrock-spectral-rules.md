---
categories:
- blackrock
description: Spectral linting rules defining API design standards and conventions for BlackRock.
layout: rules
name: BlackRock API Rules
provider_name: BlackRock
provider_slug: blackrock
rule_count: 5
rules:
- description: Portfolio requests must include a portfolioId field
  given: $.components.schemas.*.properties
  name: blackrock-portfolio-id-required
  severity: warn
- description: Date fields must use ISO 8601 date format
  given: $.components.schemas[*].properties[?(@.description =~ /date/i)]
  name: blackrock-date-format
  severity: warn
- description: Currency fields must be documented as ISO 4217
  given: $.components.schemas[*].properties.currency
  name: blackrock-currency-iso
  severity: warn
- description: All API operations must include a summary
  given: $.paths[*][*]
  name: blackrock-operations-have-summary
  severity: warn
- description: API must define at least one security scheme
  given: $.components.securitySchemes
  name: blackrock-security-defined
  severity: warn
rules_file: rules/blackrock-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/blackrock/refs/heads/main/rules/blackrock-spectral-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 5
slug: blackrock-spectral-rules
tags:
- Asset Management
- Finance
- FinTech
- Investment Management
- Portfolio Management
- Risk Analytics
- Spectral
- Linting
- API Governance
---
