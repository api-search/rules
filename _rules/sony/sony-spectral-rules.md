---
categories:
- sony
description: Spectral linting rules defining API design standards and conventions for Sony.
layout: rules
name: Sony API Rules
provider_name: Sony
provider_slug: sony
rule_count: 3
rules:
- description: Tags should be Title Case
  given: $.tags[*].name
  name: sony-tags-title-case
  severity: warn
- description: operationId should be camelCase
  given: $.paths.*.*.operationId
  name: sony-operation-id-camel-case
  severity: error
- description: Repos should declare an Apache 2.0 or MIT license
  given: $.info.license.name
  name: sony-license-required
  severity: info
rules_file: rules/sony-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sony/refs/heads/main/rules/sony-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 1
slug: sony-spectral-rules
source_filename: sony-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\nrules:\n  sony-tags-title-case:\n    description: Tags should be Title Case\n    given: $.tags[*].name\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: '^([A-Z][a-zA-Z0-9]*)( [A-Z][a-zA-Z0-9]*)*$'\n  sony-operation-id-camel-case:\n    description: operationId should be camelCase\n    given: $.paths.*.*.operationId\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n  sony-license-required:\n    description: Repos should declare an Apache 2.0 or MIT license\n    given: $.info.license.name\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: '(Apache-2\\\\.0|MIT)'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sony/refs/heads/main/rules/sony-spectral-rules.yml
tags:
- Technology
- Consumer Electronics
- Gaming
- Entertainment
- Artificial Intelligence
- Spectral
- Linting
- API Governance
---
