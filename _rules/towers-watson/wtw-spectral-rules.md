---
api_specs:
- filename: wtw-hr-portal-openapi.yml
  format: yaml
  label: WTW HR Portal
  slug: wtw-hr-portal
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/towers-watson/refs/heads/main/openapi/wtw-hr-portal-openapi.yml
categories:
- wtw
description: Spectral linting rules defining API design standards and conventions for Towers Watson.
layout: rules
name: Towers Watson API Rules
provider_name: Towers Watson
provider_slug: towers-watson
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: wtw-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: wtw-operation-summary-title-case
  severity: warn
- description: API paths must use kebab-case
  given: $.paths[*]~
  name: wtw-paths-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: wtw-must-have-tags
  severity: error
- description: All operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wtw-must-have-200-or-201
  severity: error
- description: Employee data endpoints must use authentication
  given: $.paths[/employees*][get,post,put,patch,delete]
  name: wtw-employee-data-protection
  severity: error
- description: List operations should support pagination
  given: $.paths[*][get][?(@.operationId =~ /^list/)]
  name: wtw-pagination-required
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: wtw-responses-must-have-description
  severity: error
rules_file: rules/wtw-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/towers-watson/refs/heads/main/rules/wtw-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: wtw-spectral-rules
source_filename: wtw-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  wtw-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  wtw-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  wtw-paths-kebab-case:\n    description: API paths must use kebab-case\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-]+|/\\\\{[a-zA-Z0-9]+\\\\})*$\"\n\n  wtw-must-have-tags:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  wtw-must-have-200-or-201:\n\
  \    description: All operations must define a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  wtw-employee-data-protection:\n    description: Employee data endpoints must use authentication\n    severity: error\n    given: \"$.paths[/employees*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  wtw-pagination-required:\n    description: List operations should support pagination\n    severity: warn\n    given: \"$.paths[*][get][?(@.operationId =~ /^list/)]\"\n    then:\n      field: parameters\n      function: truthy\n\n  wtw-responses-must-have-description:\n    description: All responses must have a description\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function:\
  \ truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/towers-watson/refs/heads/main/rules/wtw-spectral-rules.yml
tags:
- Human Resources
- Risk Management
- Benefits
- Consulting
- Actuarial
- Insurance Brokerage
- Human Capital
- Spectral
- Linting
- API Governance
---
