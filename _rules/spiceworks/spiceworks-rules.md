---
api_specs:
- filename: spiceworks-cloud-apps-openapi.yml
  format: yaml
  label: Spiceworks Cloud Apps API
  slug: spiceworks-cloud-apps-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spiceworks/refs/heads/main/openapi/spiceworks-cloud-apps-openapi.yml
categories:
- spiceworks
description: Spectral linting rules defining API design standards and conventions for Spiceworks.
layout: rules
name: Spiceworks API Rules
provider_name: Spiceworks
provider_slug: spiceworks
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spiceworks-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spiceworks-tags-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spiceworks-operation-tags
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spiceworks-operation-id
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: spiceworks-operation-description
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: spiceworks-path-kebab-case
  severity: warn
- description: GET operations must define a 200 response schema
  given: $.paths[*].get.responses.200.content
  name: spiceworks-response-200-schema
  severity: warn
- description: All operations should have security defined
  given: $.paths[*][get,post,put,patch,delete]
  name: spiceworks-security-defined
  severity: warn
rules_file: rules/spiceworks-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spiceworks/refs/heads/main/rules/spiceworks-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: spiceworks-rules
source_filename: spiceworks-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spiceworks-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spiceworks-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spiceworks-operation-tags:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spiceworks-operation-id:\n\
  \    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spiceworks-operation-description:\n    description: All operations must have a description\n    message: Operation should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  spiceworks-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: Path segment \"{{value}}\" should use kebab-case (lowercase with hyphens)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{][a-z0-9_{}/-]*)*$\"\n\n  spiceworks-response-200-schema:\n    description: GET operations must define a 200 response schema\n    message: GET operation should define\
  \ a 200 response with a schema\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content\"\n    then:\n      function: truthy\n\n  spiceworks-security-defined:\n    description: All operations should have security defined\n    message: Operation should define security requirements\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spiceworks/refs/heads/main/rules/spiceworks-rules.yml
tags:
- Community
- Enterprise IT
- IT Management
- Spectral
- Linting
- API Governance
---
