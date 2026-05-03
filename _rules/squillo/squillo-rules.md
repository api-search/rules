---
api_specs:
- filename: squillo-platform-openapi.yml
  format: yaml
  label: Squillo Platform API
  slug: squillo-platform
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squillo/refs/heads/main/openapi/squillo-platform-openapi.yml
categories:
- squillo
description: Spectral linting rules defining API design standards and conventions for Squillo.
layout: rules
name: Squillo API Rules
provider_name: Squillo
provider_slug: squillo
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: squillo-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: squillo-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: squillo-tags-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][*].description
  name: squillo-description-required
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][*].responses
  name: squillo-response-200-or-201-required
  severity: error
- description: Path segments should use kebab-case
  given: $.paths
  name: squillo-paths-use-kebab-case
  severity: warn
- description: Response schemas should use $ref
  given: $.paths[*][*].responses[*].content[*].schema
  name: squillo-no-inline-schemas-in-responses
  severity: hint
rules_file: rules/squillo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/squillo/refs/heads/main/rules/squillo-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 4
slug: squillo-rules
source_filename: squillo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  squillo-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s?)+$\"\n\n  squillo-operationid-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  squillo-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  squillo-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  squillo-response-200-or-201-required:\n    description:\
  \ All operations must define a success response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['202']\n            - required: ['204']\n\n  squillo-paths-use-kebab-case:\n    description: Path segments should use kebab-case\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}\\\\-]*)+$\"\n\n  squillo-no-inline-schemas-in-responses:\n    description: Response schemas should use $ref\n    severity: hint\n    given: \"$.paths[*][*].responses[*].content[*].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['$ref']\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/squillo/refs/heads/main/rules/squillo-rules.yml
tags:
- Integration Platform
- Automation
- Workflow
- No-Code
- IT Process Automation
- Software As A Utility
- Spectral
- Linting
- API Governance
---
