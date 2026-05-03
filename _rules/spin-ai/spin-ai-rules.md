---
api_specs:
- filename: spin-ai-openapi.yml
  format: yaml
  label: Spin.AI SpinOne API
  slug: spin-ai-spinone-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spin-ai/refs/heads/main/openapi/spin-ai-openapi.yml
categories:
- spin
description: Spectral linting rules defining API design standards and conventions for Spin.AI.
layout: rules
name: Spin.AI API Rules
provider_name: Spin.AI
provider_slug: spin-ai
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spin-ai-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spin-ai-tags-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-ai-operation-id
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-ai-operation-tags
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-ai-operation-description
  severity: warn
- description: All API paths should be versioned with /api/v1/ prefix
  given: $.paths[*]~
  name: spin-ai-path-versioned
  severity: warn
- description: All operations must require authentication
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-ai-security-required
  severity: error
- description: POST and PUT operations must have a request body schema
  given: $.paths[*][post,put].requestBody
  name: spin-ai-request-body-schema
  severity: warn
rules_file: rules/spin-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spin-ai/refs/heads/main/rules/spin-ai-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: spin-ai-rules
source_filename: spin-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spin-ai-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spin-ai-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spin-ai-operation-id:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spin-ai-operation-tags:\n\
  \    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spin-ai-operation-description:\n    description: All operations must have a description\n    message: Operation should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  spin-ai-path-versioned:\n    description: All API paths should be versioned with /api/v1/ prefix\n    message: Path should be versioned (e.g. /api/v1/)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+\"\n\n  spin-ai-security-required:\n    description: All operations must require authentication\n    message: Operation must define security requirements (Spin.AI requires SPIN_API key)\n\
  \    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  spin-ai-request-body-schema:\n    description: POST and PUT operations must have a request body schema\n    message: POST/PUT operation should have a request body with schema\n    severity: warn\n    given: \"$.paths[*][post,put].requestBody\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spin-ai/refs/heads/main/rules/spin-ai-rules.yml
tags:
- Backup
- Compliance
- Data Protection
- Ransomware
- SaaS Security
- Spectral
- Linting
- API Governance
---
