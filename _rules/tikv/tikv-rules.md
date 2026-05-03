---
api_specs:
- filename: tikv-http-api-openapi.yml
  format: yaml
  label: TiKV HTTP Management API
  slug: tikv-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tikv/refs/heads/main/openapi/tikv-http-api-openapi.yml
categories:
- tikv
description: Spectral linting rules defining API design standards and conventions for TiKV.
layout: rules
name: TiKV API Rules
provider_name: TiKV
provider_slug: tikv
rule_count: 4
rules:
- description: All operations must have a summary
  given: $.paths[*][*]
  name: tikv-operation-summary
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: tikv-operation-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: tikv-operation-id
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: tikv-response-description
  severity: warn
rules_file: rules/tikv-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tikv/refs/heads/main/rules/tikv-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 2
slug: tikv-rules
source_filename: tikv-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tikv-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tikv-operation-tags:\n    description: All operations must have tags\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tikv-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tikv-response-description:\n    description: All responses must have a description\n    message: \"Response must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n \
  \     function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tikv/refs/heads/main/rules/tikv-rules.yml
tags:
- ACID
- CNCF
- Database
- Distributed Systems
- Key-Value Store
- Open Source
- Rust
- Spectral
- Linting
- API Governance
---
