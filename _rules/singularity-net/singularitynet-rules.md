---
api_specs:
- filename: singularitynet-marketplace-openapi.yml
  format: yaml
  label: SingularityNET Daemon API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/singularity-net/refs/heads/main/openapi/singularitynet-marketplace-openapi.yml
categories:
- singularitynet
description: Spectral linting rules defining API design standards and conventions for SingularityNET.
layout: rules
name: SingularityNET API Rules
provider_name: SingularityNET
provider_slug: singularity-net
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: singularitynet-operation-summary-title-case
  severity: warn
- description: Operation IDs should use camelCase.
  given: $.paths[*][*].operationId
  name: singularitynet-operation-ids-camel-case
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: singularitynet-tags-required
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][*]
  name: singularitynet-description-required
  severity: warn
- description: Successful operations must define a 200 response.
  given: $.paths[*][*].responses
  name: singularitynet-response-200-required
  severity: error
- description: Response bodies should use a data envelope wrapper.
  given: $.paths[*][*].responses['200'].content['application/json'].schema.properties
  name: singularitynet-data-envelope
  severity: info
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in == "path")]
  name: singularitynet-path-params-described
  severity: warn
rules_file: rules/singularitynet-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/singularity-net/refs/heads/main/rules/singularitynet-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 5
slug: singularitynet-rules
source_filename: singularitynet-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  singularitynet-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: 'Summary \"{{value}}\" must use Title Case.'\n    severity: warn\n    given: '$.paths[*][*].summary'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-z]+(\\s[A-Z][a-z]+)*$'\n\n  singularitynet-operation-ids-camel-case:\n    description: Operation IDs should use camelCase.\n    message: 'OperationId \"{{value}}\" should be camelCase.'\n    severity: warn\n    given: '$.paths[*][*].operationId'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  singularitynet-tags-required:\n    description: All operations must include at least one tag.\n    message: Operation must include at least one tag.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: defined\n\n  singularitynet-description-required:\n \
  \   description: All operations must have a description.\n    message: Operation must include a description.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: description\n      function: defined\n\n  singularitynet-response-200-required:\n    description: Successful operations must define a 200 response.\n    message: Operation must define a 200 success response.\n    severity: error\n    given: '$.paths[*][*].responses'\n    then:\n      field: '200'\n      function: defined\n\n  singularitynet-data-envelope:\n    description: Response bodies should use a data envelope wrapper.\n    message: Response body should wrap content in a data property.\n    severity: info\n    given: \"$.paths[*][*].responses['200'].content['application/json'].schema.properties\"\n    then:\n      field: data\n      function: defined\n\n  singularitynet-path-params-described:\n    description: All path parameters must have descriptions.\n    message: Path parameter must have a description.\n\
  \    severity: warn\n    given: '$.paths[*][*].parameters[?(@.in == \"path\")]'\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/singularity-net/refs/heads/main/rules/singularitynet-rules.yml
tags:
- Artificial Intelligence
- Blockchain
- Decentralized AI
- AI Marketplace
- Web3
- Spectral
- Linting
- API Governance
---
