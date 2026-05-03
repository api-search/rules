---
api_specs:
- filename: silverpop-openapi.yml
  format: yaml
  label: Silverpop Engage XML API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/silverpop/refs/heads/main/openapi/silverpop-openapi.yml
categories:
- silverpop
description: Spectral linting rules defining API design standards and conventions for Silverpop.
layout: rules
name: Silverpop API Rules
provider_name: Silverpop
provider_slug: silverpop
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: silverpop-operation-summary-title-case
  severity: warn
- description: Operation IDs should use camelCase.
  given: $.paths[*][*].operationId
  name: silverpop-operation-ids-camel-case
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: silverpop-tags-defined
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][*]
  name: silverpop-description-required
  severity: warn
- description: All operations must define a 200 success response.
  given: $.paths[*][*].responses
  name: silverpop-response-200-required
  severity: error
- description: Non-authentication operations must use BearerAuth.
  given: $.paths[?(!@property.match(/oauth/))][*]
  name: silverpop-bearer-auth
  severity: warn
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in == "path")]
  name: silverpop-path-parameters-described
  severity: warn
rules_file: rules/silverpop-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/silverpop/refs/heads/main/rules/silverpop-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 6
slug: silverpop-rules
source_filename: silverpop-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  silverpop-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: 'Summary \"{{value}}\" must use Title Case.'\n    severity: warn\n    given: '$.paths[*][*].summary'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-z]+(\\s[A-Z][a-z]+)*$'\n\n  silverpop-operation-ids-camel-case:\n    description: Operation IDs should use camelCase.\n    message: 'OperationId \"{{value}}\" should be camelCase.'\n    severity: warn\n    given: '$.paths[*][*].operationId'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  silverpop-tags-defined:\n    description: All operations must include at least one tag.\n    message: Operation must include at least one tag.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: defined\n\n  silverpop-description-required:\n    description: All operations\
  \ must have a description.\n    message: Operation must include a description.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: description\n      function: defined\n\n  silverpop-response-200-required:\n    description: All operations must define a 200 success response.\n    message: Operation must define a 200 response.\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      field: '200'\n      function: defined\n\n  silverpop-bearer-auth:\n    description: Non-authentication operations must use BearerAuth.\n    message: Operation must declare BearerAuth security.\n    severity: warn\n    given: '$.paths[?(!@property.match(/oauth/))][*]'\n    then:\n      field: security\n      function: defined\n\n  silverpop-path-parameters-described:\n    description: All path parameters must have descriptions.\n    message: Path parameter \"{{value}}\" must have a description.\n    severity: warn\n    given: '$.paths[*][*].parameters[?(@.in == \"path\"\
  )]'\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/silverpop/refs/heads/main/rules/silverpop-rules.yml
tags:
- Email Marketing
- Marketing Automation
- Campaign Management
- Digital Marketing
- Spectral
- Linting
- API Governance
---
