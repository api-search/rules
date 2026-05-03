---
api_specs:
- filename: simscale-openapi.yml
  format: yaml
  label: SimScale REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/simscale/refs/heads/main/openapi/simscale-openapi.yml
categories:
- simscale
description: Spectral linting rules defining API design standards and conventions for SimScale.
layout: rules
name: SimScale API Rules
provider_name: SimScale
provider_slug: simscale
rule_count: 9
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: simscale-operation-summary-title-case
  severity: warn
- description: Operation IDs should use camelCase.
  given: $.paths[*][*].operationId
  name: simscale-operation-ids-camel-case
  severity: warn
- description: All operations must use X-API-KEY authentication.
  given: $.paths[*][*]
  name: simscale-api-key-required
  severity: warn
- description: All paths must be prefixed with /v0/.
  given: $.paths[*]~
  name: simscale-path-v0-prefix
  severity: error
- description: Successful operations must define 200 or 201 response.
  given: $.paths[*][*].responses
  name: simscale-response-200-or-201
  severity: error
- description: All operations must have a description.
  given: $.paths[*][*]
  name: simscale-description-required
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: simscale-tags-required
  severity: warn
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in == "path")]
  name: simscale-path-params-described
  severity: warn
- description: Schema property names should use camelCase (SimScale SDK convention).
  given: $.components.schemas[*].properties[*]~
  name: simscale-schemas-use-camel-case
  severity: info
rules_file: rules/simscale-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/simscale/refs/heads/main/rules/simscale-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: simscale-rules
source_filename: simscale-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  simscale-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: 'Summary \"{{value}}\" must use Title Case.'\n    severity: warn\n    given: '$.paths[*][*].summary'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-z]+(\\s[A-Z][a-z]+)*$'\n\n  simscale-operation-ids-camel-case:\n    description: Operation IDs should use camelCase.\n    message: 'OperationId \"{{value}}\" should be camelCase.'\n    severity: warn\n    given: '$.paths[*][*].operationId'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  simscale-api-key-required:\n    description: All operations must use X-API-KEY authentication.\n    message: Operation must declare ApiKeyAuth security.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: security\n      function: defined\n\n  simscale-path-v0-prefix:\n    description: All\
  \ paths must be prefixed with /v0/.\n    message: 'Path \"{{value}}\" must start with /v0/.'\n    severity: error\n    given: '$.paths[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/v0/'\n\n  simscale-response-200-or-201:\n    description: Successful operations must define 200 or 201 response.\n    message: Operation must define a 200 or 201 success response.\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n          - required: ['200']\n          - required: ['201']\n\n  simscale-description-required:\n    description: All operations must have a description.\n    message: Operation must include a description.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: description\n      function: defined\n\n  simscale-tags-required:\n    description: All operations must include at least one tag.\n    message: Operation must include\
  \ at least one tag.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: defined\n\n  simscale-path-params-described:\n    description: All path parameters must have descriptions.\n    message: Path parameter must have a description.\n    severity: warn\n    given: '$.paths[*][*].parameters[?(@.in == \"path\")]'\n    then:\n      field: description\n      function: defined\n\n  simscale-schemas-use-camel-case:\n    description: Schema property names should use camelCase (SimScale SDK convention).\n    message: 'Schema property \"{{value}}\" should use camelCase.'\n    severity: info\n    given: '$.components.schemas[*].properties[*]~'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/simscale/refs/heads/main/rules/simscale-rules.yml
tags:
- CAE
- CFD
- FEA
- Simulation
- Engineering
- Spectral
- Linting
- API Governance
---
