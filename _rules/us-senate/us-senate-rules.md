---
api_specs:
- filename: us-senate-lda-openapi.yml
  format: yaml
  label: Senate Lobbying Disclosure Act (LDA) API
  slug: lda-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-senate/refs/heads/main/openapi/us-senate-lda-openapi.yml
categories:
- lda
description: Spectral linting rules defining API design standards and conventions for US Senate.
layout: rules
name: US Senate API Rules
provider_name: US Senate
provider_slug: us-senate
rule_count: 7
rules:
- description: LDA API paths end with a trailing slash
  given: $.paths[*]~
  name: lda-path-trailing-slash
  severity: info
- description: LDA API GET operations should support a format parameter
  given: $.paths[*].get
  name: lda-format-parameter
  severity: info
- description: All operations must have a summary
  given: $.paths[*][*]
  name: lda-operation-summary-required
  severity: error
- description: List endpoints must return paginated responses with count/next/previous
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: lda-list-endpoints-paginated
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][*]
  name: lda-operation-tags
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: lda-get-200-response
  severity: error
- description: Path parameters must have description
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: lda-path-params-documented
  severity: warn
rules_file: rules/us-senate-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-senate/refs/heads/main/rules/us-senate-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 3
slug: us-senate-rules
source_filename: us-senate-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  # LDA API-specific rules\n  lda-path-trailing-slash:\n    description: LDA API paths end with a trailing slash\n    message: \"Path '{{property}}' should end with a trailing slash\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/$\"\n\n  lda-format-parameter:\n    description: LDA API GET operations should support a format parameter\n    message: \"GET operation should document the 'format' query parameter\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: truthy\n\n  lda-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  lda-list-endpoints-paginated:\n    description: List endpoints must return paginated responses with count/next/previous\n\
  \    message: \"List response schema should include count, next, previous, and results\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n\n  lda-operation-tags:\n    description: Operations must have at least one tag\n    message: \"Operation has no tags\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  lda-get-200-response:\n    description: All GET operations must define a 200 response\n    message: \"GET operation missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  lda-path-params-documented:\n    description: Path parameters must have description\n    message: \"Path parameter missing description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-senate/refs/heads/main/rules/us-senate-rules.yml
tags:
- Federal Government
- Lobbying
- Government Transparency
- Campaign Finance
- Open Data
- Spectral
- Linting
- API Governance
---
