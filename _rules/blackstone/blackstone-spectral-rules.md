---
categories:
- blackstone
description: Spectral linting rules defining API design standards and conventions for Blackstone.
layout: rules
name: Blackstone API Rules
provider_name: Blackstone
provider_slug: blackstone
rule_count: 5
rules:
- description: Fund strategy must be one of the defined values
  given: $.components.schemas.Fund.properties.strategy
  name: blackstone-fund-strategy-enum
  severity: warn
- description: Financial records must include a currency field
  given: $.components.schemas[*].properties
  name: blackstone-currency-required
  severity: warn
- description: Date fields must use ISO 8601 format
  given: $.components.schemas[*].properties[?(@.description =~ /date/i)]
  name: blackstone-date-iso-format
  severity: warn
- description: All API operations should include descriptions
  given: $.paths[*][*]
  name: blackstone-operations-have-descriptions
  severity: warn
- description: All ID fields should be of type string
  given: $.components.schemas[*].properties[?(@.description =~ /identifier|id/i)]
  name: blackstone-ids-are-strings
  severity: warn
rules_file: rules/blackstone-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/blackstone/refs/heads/main/rules/blackstone-spectral-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 5
slug: blackstone-spectral-rules
tags:
- Alternative Assets
- Finance
- Investment Management
- Private Equity
- Real Estate
- Spectral
- Linting
- API Governance
---
