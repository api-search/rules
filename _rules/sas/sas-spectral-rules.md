---
api_specs:
- filename: sas-viya-rest-api-openapi.yml
  format: yaml
  label: SAS Viya REST API
  slug: viya-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sas/refs/heads/main/openapi/sas-viya-rest-api-openapi.yml
categories:
- sas
description: Spectral linting rules defining API design standards and conventions for SAS Institute.
layout: rules
name: SAS Institute API Rules
provider_name: SAS Institute
provider_slug: sas
rule_count: 5
rules:
- description: Tags should be in Title Case (e.g., Decisions, Reports)
  given: $.tags[*].name
  name: sas-tags-title-case
  severity: warn
- description: operationId should be camelCase
  given: $.paths.*.*.operationId
  name: sas-operation-id-camel-case
  severity: error
- description: Operation summaries should use Title Case
  given: $.paths.*.*.summary
  name: sas-summary-title-case
  severity: warn
- description: Operations should be secured via OAuth via SAS Logon
  given: $.paths.*.*
  name: sas-oauth-required
  severity: warn
- description: SAS Viya uses application/vnd.sas.* vendor media types for resources
  given: $.paths.*.*.responses.*.content
  name: sas-vendor-media-type
  severity: info
rules_file: rules/sas-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sas/refs/heads/main/rules/sas-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 3
slug: sas-spectral-rules
source_filename: sas-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\nrules:\n  sas-tags-title-case:\n    description: Tags should be in Title Case (e.g., Decisions, Reports)\n    given: $.tags[*].name\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: '^([A-Z][a-zA-Z0-9]*)( [A-Z][a-zA-Z0-9]*)*$'\n  sas-operation-id-camel-case:\n    description: operationId should be camelCase\n    given: $.paths.*.*.operationId\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n  sas-summary-title-case:\n    description: Operation summaries should use Title Case\n    given: $.paths.*.*.summary\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z]'\n  sas-oauth-required:\n    description: Operations should be secured via OAuth via SAS Logon\n    given: $.paths.*.*\n    severity: warn\n    then:\n      field: security\n      function: truthy\n  sas-vendor-media-type:\n\
  \    description: SAS Viya uses application/vnd.sas.* vendor media types for resources\n    given: $.paths.*.*.responses.*.content\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: 'application/vnd\\\\.sas\\\\.'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sas/refs/heads/main/rules/sas-spectral-rules.yml
tags:
- Analytics
- Data Management
- Artificial Intelligence
- Machine Learning
- Software
- Spectral
- Linting
- API Governance
---
