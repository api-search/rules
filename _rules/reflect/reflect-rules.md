---
api_specs:
- filename: reflect-openapi.yml
  format: yaml
  label: Reflect
  slug: reflect
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reflect/refs/heads/main/openapi/reflect-openapi.yml
categories:
- reflect
description: Spectral linting rules defining API design standards and conventions for Reflect.
layout: rules
name: Reflect API Rules
provider_name: Reflect
provider_slug: reflect
rule_count: 6
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: reflect-operation-summary-title-case
  severity: warn
- description: Reflect API uses X-API-KEY header authentication.
  given: $.components.securitySchemes[*][?(@.type=='apiKey')]
  name: reflect-api-key-auth
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: reflect-tags-defined
  severity: warn
- description: API must define at least one server.
  given: $
  name: reflect-servers-defined
  severity: error
- description: All operations must define a 200 success response.
  given: $.paths[*][*].responses
  name: reflect-response-200-defined
  severity: error
- description: Reflect uses integer IDs for tests and executions (not UUIDs). Path parameters should reflect this.
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: reflect-integer-ids
  severity: info
rules_file: rules/reflect-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reflect/refs/heads/main/rules/reflect-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 3
slug: reflect-rules
source_filename: reflect-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  reflect-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 '\\\\-]*$\"\n\n  reflect-api-key-auth:\n    description: Reflect API uses X-API-KEY header authentication.\n    message: \"Security scheme must use apiKey in header with name X-API-KEY.\"\n    severity: warn\n    given: \"$.components.securitySchemes[*][?(@.type=='apiKey')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^X-API-KEY$\"\n\n  reflect-tags-defined:\n    description: All operations must include at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  reflect-servers-defined:\n    description: API must define at least one server.\n    message: \"API must have at least one server defined.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  reflect-response-200-defined:\n    description: All operations must define a 200 success response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n\n  reflect-integer-ids:\n    description: >-\n      Reflect uses integer IDs for tests and executions (not UUIDs).\n      Path parameters should reflect this.\n    message: \"Path parameter for ID should use type integer.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [\"integer\"\
  , \"string\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reflect/refs/heads/main/rules/reflect-rules.yml
tags:
- AI Testing
- Artificial Intelligence
- Automated Testing
- CI/CD
- End-to-End Testing
- QA
- Testing
- Spectral
- Linting
- API Governance
---
