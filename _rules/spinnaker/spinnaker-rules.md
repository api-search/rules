---
api_specs:
- filename: spinnaker-gate-openapi.yml
  format: yaml
  label: Spinnaker Gate API
  slug: spinnaker-gate-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spinnaker/refs/heads/main/openapi/spinnaker-gate-openapi.yml
categories:
- spinnaker
description: Spectral linting rules defining API design standards and conventions for Spinnaker.
layout: rules
name: Spinnaker API Rules
provider_name: Spinnaker
provider_slug: spinnaker
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spinnaker-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spinnaker-tags-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spinnaker-operation-id
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spinnaker-operation-tags
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: spinnaker-operation-description
  severity: warn
- description: Application-scoped paths must include {application} parameter
  given: $.paths./applications/{application}[*]~
  name: spinnaker-application-path-structure
  severity: info
- description: GET operations must define response schemas
  given: $.paths[*].get.responses.200
  name: spinnaker-get-response-schema
  severity: warn
- description: API should have security schemes defined
  given: $.components.securitySchemes
  name: spinnaker-security-defined
  severity: warn
rules_file: rules/spinnaker-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spinnaker/refs/heads/main/rules/spinnaker-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: spinnaker-rules
source_filename: spinnaker-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spinnaker-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spinnaker-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spinnaker-operation-id:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spinnaker-operation-tags:\n\
  \    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spinnaker-operation-description:\n    description: All operations should have a description\n    message: Operation should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  spinnaker-application-path-structure:\n    description: Application-scoped paths must include {application} parameter\n    message: Application-scoped paths should use /applications/{application}/ prefix\n    severity: info\n    given: \"$.paths./applications/{application}[*]~\"\n    then:\n      function: defined\n\n  spinnaker-get-response-schema:\n    description: GET operations must define response schemas\n    message: GET operation should define a response schema\n\
  \    severity: warn\n    given: \"$.paths[*].get.responses.200\"\n    then:\n      function: truthy\n\n  spinnaker-security-defined:\n    description: API should have security schemes defined\n    message: Security schemes should be defined for Spinnaker Gate authentication\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spinnaker/refs/heads/main/rules/spinnaker-rules.yml
tags:
- Continuous Delivery
- Containers
- DevOps
- Multi-Cloud
- Pipelines
- Spectral
- Linting
- API Governance
---
