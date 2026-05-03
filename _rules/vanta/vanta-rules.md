---
api_specs:
- filename: vanta-openapi.yml
  format: yaml
  label: Vanta API
  slug: vanta-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vanta/refs/heads/main/openapi/vanta-openapi.yml
- filename: vanta-auditor-openapi.yml
  format: yaml
  label: Vanta Auditor API
  slug: vanta-auditor-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vanta/refs/heads/main/openapi/vanta-auditor-openapi.yml
categories:
- vanta
description: Spectral linting rules defining API design standards and conventions for Vanta.
layout: rules
name: Vanta API Rules
provider_name: Vanta
provider_slug: vanta
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: vanta-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: vanta-operation-ids-present
  severity: error
- description: All data paths must be versioned with /v1/ prefix
  given: $.paths
  name: vanta-paths-versioned
  severity: warn
- description: List endpoints must support pageSize query parameter
  given: $.paths[*].get.parameters[?(@.name=='pageSize')]
  name: vanta-pagination-page-size
  severity: warn
- description: Successful responses must define a content schema
  given: $.paths[*][*].responses.200
  name: vanta-responses-have-content
  severity: warn
- description: All operations should document their security requirements
  given: $.paths[*][*]
  name: vanta-auth-documented
  severity: warn
- description: All operations must define 401 Unauthorized response
  given: $.paths[*][*].responses
  name: vanta-error-responses-defined
  severity: warn
- description: POST operations must have a request body
  given: $.paths[*].post
  name: vanta-request-body-for-post
  severity: error
- description: Operation tags must match defined tag list
  given: $.paths[*][*].tags[*]
  name: vanta-tags-singular-or-plural-consistent
  severity: warn
- description: Path parameters must be defined in the path segment
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: vanta-path-params-in-path
  severity: error
rules_file: rules/vanta-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vanta/refs/heads/main/rules/vanta-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: vanta-rules
source_filename: vanta-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vanta-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  vanta-operation-ids-present:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  vanta-paths-versioned:\n    description: All data paths must be versioned with /v1/ prefix\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v1\\\\/\"\n\n  vanta-pagination-page-size:\n    description: List endpoints must support pageSize query parameter\n    severity: warn\n    given: \"$.paths[*].get.parameters[?(@.name=='pageSize')]\"\n    then:\n      field: schema.maximum\n      function: defined\n\n  vanta-responses-have-content:\n\
  \    description: Successful responses must define a content schema\n    severity: warn\n    given: \"$.paths[*][*].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  vanta-auth-documented:\n    description: All operations should document their security requirements\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  vanta-error-responses-defined:\n    description: All operations must define 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  vanta-request-body-for-post:\n    description: POST operations must have a request body\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  vanta-tags-singular-or-plural-consistent:\n    description: Operation tags must match defined tag list\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n  \
  \  then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Authentication\n          - Users\n          - Vulnerabilities\n          - Controls\n          - Tests\n          - Documents\n          - Vendors\n          - Resources\n          - Integrations\n\n  vanta-path-params-in-path:\n    description: Path parameters must be defined in the path segment\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: required\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vanta/refs/heads/main/rules/vanta-rules.yml
tags:
- Cybersecurity
- Compliance
- Security
- Governance
- Risk Management
- Spectral
- Linting
- API Governance
---
