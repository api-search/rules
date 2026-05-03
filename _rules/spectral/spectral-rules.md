---
categories:
- spectral
description: Spectral linting rules defining API design standards and conventions for Spectral.
layout: rules
name: Spectral API Rules
provider_name: Spectral
provider_slug: spectral
rule_count: 4
rules:
- description: Spectral rulesets should extend a base ruleset or define rules explicitly.
  given: $
  name: spectral-ruleset-has-extends
  severity: hint
- description: Every Spectral rule should include a description for documentation clarity.
  given: $.rules[*]
  name: spectral-rule-has-description
  severity: warn
- description: Every Spectral rule should include a message template for helpful output.
  given: $.rules[*]
  name: spectral-rule-has-message
  severity: warn
- description: Every Spectral rule should explicitly declare its severity level.
  given: $.rules[*]
  name: spectral-rule-has-severity
  severity: hint
rules_file: rules/spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spectral/refs/heads/main/rules/spectral-rules.yml
severity_counts:
  error: 0
  hint: 2
  info: 0
  warn: 2
slug: spectral-rules
source_filename: spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  spectral-ruleset-has-extends:\n    description: Spectral rulesets should extend a base ruleset or define rules explicitly.\n    message: \"Ruleset at {{path}} should extend a base ruleset (e.g., spectral:oas).\"\n    severity: hint\n    given: \"$\"\n    then:\n      field: extends\n      function: truthy\n\n  spectral-rule-has-description:\n    description: Every Spectral rule should include a description for documentation clarity.\n    message: \"Rule {{path}} is missing a description.\"\n    severity: warn\n    given: \"$.rules[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spectral-rule-has-message:\n    description: Every Spectral rule should include a message template for helpful output.\n    message: \"Rule {{path}} is missing a message template.\"\n    severity: warn\n    given: \"$.rules[*]\"\n    then:\n      field: message\n      function: truthy\n\n  spectral-rule-has-severity:\n    description: Every\
  \ Spectral rule should explicitly declare its severity level.\n    message: \"Rule {{path}} should declare an explicit severity.\"\n    severity: hint\n    given: \"$.rules[*]\"\n    then:\n      field: severity\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spectral/refs/heads/main/rules/spectral-rules.yml
tags:
- API Design
- API Linting
- API Style Guide
- AsyncAPI
- JSON Schema
- OpenAPI
- Quality Assurance
- Spectral
- Linting
- API Governance
---
