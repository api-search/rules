---
api_specs:
- filename: smartbear-swaggerhub-openapi.yml
  format: yaml
  label: SwaggerHub API
  slug: swaggerhub
  spec_type: OpenAPI
  url: https://openapi/smartbear-swaggerhub-openapi.yml
categories:
- smartbear
description: Spectral linting rules defining API design standards and conventions for SmartBear.
layout: rules
name: SmartBear API Rules
provider_name: SmartBear
provider_slug: smartbear
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: smartbear-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case or path parameter placeholders
  given: $.paths[*]~
  name: smartbear-path-kebab-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smartbear-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: smartbear-api-tags-required
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: smartbear-response-200-defined
  severity: error
- description: All operations should have security defined at spec or operation level
  given: $.paths[*][*]
  name: smartbear-security-defined
  severity: warn
- description: All parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: smartbear-parameter-description
  severity: warn
- description: API paths should follow hierarchical owner/resource/id pattern
  given: $.paths[*]~
  name: smartbear-hierarchical-paths
  severity: info
rules_file: rules/smartbear-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smartbear/refs/heads/main/rules/smartbear-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: smartbear-rules
source_filename: smartbear-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SmartBear API Naming Conventions\n  smartbear-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' should use camelCase (e.g., getOwnerApis)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  smartbear-path-kebab-case:\n    description: Path segments must use kebab-case or path parameter placeholders\n    message: \"Path segment should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\}))*$\"\n\n  smartbear-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z]*(\\\\s[A-Z][A-Za-z]*)*$\"\n\n  smartbear-api-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smartbear-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: \"GET operations must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  smartbear-security-defined:\n    description: All operations should have security defined at spec or operation level\n    message: \"Operations should define security requirements\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required:\
  \ [security]\n            - not:\n                required: [security]\n\n  smartbear-parameter-description:\n    description: All parameters should have descriptions\n    message: \"Parameter '{{value}}' should include a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  smartbear-hierarchical-paths:\n    description: API paths should follow hierarchical owner/resource/id pattern\n    message: \"Paths should follow /{owner}/{resource}/{id} hierarchy\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/[a-z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smartbear/refs/heads/main/rules/smartbear-rules.yml
tags:
- API Design
- API Documentation
- API Testing
- Contract Testing
- Governance
- Monitoring
- Platform
- Spectral
- Linting
- API Governance
---
