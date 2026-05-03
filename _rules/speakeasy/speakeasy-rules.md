---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Speakeasy
  slug: speakeasy
  spec_type: OpenAPI
  url: https://www.speakeasy.com/openapi.yaml
categories:
- speakeasy
description: Spectral linting rules defining API design standards and conventions for Speakeasy.
layout: rules
name: Speakeasy API Rules
provider_name: Speakeasy
provider_slug: speakeasy
rule_count: 9
rules:
- description: All API paths must be prefixed with /v1/
  given: $.paths.*~
  name: speakeasy-path-versioned
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths.*.*.operationId
  name: speakeasy-operation-id-camel-case
  severity: warn
- description: All operations must define an operationId
  given: $.paths.*[get,post,put,patch,delete]
  name: speakeasy-operation-id-required
  severity: error
- description: All operations must have at least one tag for grouping
  given: $.paths.*[get,post,put,patch,delete]
  name: speakeasy-operation-tags-required
  severity: warn
- description: All operations must have a summary in Title Case
  given: $.paths.*[get,post,put,patch,delete]
  name: speakeasy-operation-summary-required
  severity: warn
- description: Operations should define 4XX error responses
  given: $.paths.*[get,post,put,patch,delete].responses
  name: speakeasy-error-responses-required
  severity: warn
- description: Path parameters should use camelCase naming (e.g., workspaceId not workspace_id)
  given: $.paths.*.*.parameters[?(@.in == 'path')].name
  name: speakeasy-path-param-camel-case
  severity: info
- description: API operations should define security requirements
  given: $.paths.*[get,post,put,patch,delete]
  name: speakeasy-security-defined
  severity: warn
- description: Workspace-scoped paths should use the /workspace/{workspace_id}/ prefix
  given: $.paths.*~
  name: speakeasy-workspace-paths-consistent
  severity: info
rules_file: rules/speakeasy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/speakeasy/refs/heads/main/rules/speakeasy-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: speakeasy-rules
source_filename: speakeasy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # All paths must start with /v1/\n  speakeasy-path-versioned:\n    description: All API paths must be prefixed with /v1/\n    severity: error\n    given: \"$.paths.*~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  # Operation IDs must be camelCase\n  speakeasy-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have an operationId\n  speakeasy-operation-id-required:\n    description: All operations must define an operationId\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # All operations must have at least one tag\n  speakeasy-operation-tags-required:\n    description: All operations must have at\
  \ least one tag for grouping\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # All operations must have a summary\n  speakeasy-operation-summary-required:\n    description: All operations must have a summary in Title Case\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Responses must define 4XX error handling\n  speakeasy-error-responses-required:\n    description: Operations should define 4XX error responses\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"4XX\"]\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n\n  # Resource IDs should use camelCase path parameters\n \
  \ speakeasy-path-param-camel-case:\n    description: Path parameters should use camelCase naming (e.g., workspaceId not workspace_id)\n    severity: info\n    given: \"$.paths.*.*.parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-zA-Z][a-zA-Z0-9]*([A-Z][a-zA-Z0-9]*)*$\"\n\n  # Security must be defined at operation or global level\n  speakeasy-security-defined:\n    description: API operations should define security requirements\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"security\"]\n            - properties:\n                security:\n                  type: array\n\n  # Workspace-scoped paths should consistently reference workspace_id\n  speakeasy-workspace-paths-consistent:\n    description: Workspace-scoped paths should use the /workspace/{workspace_id}/ prefix\n \
  \   severity: info\n    given: \"$.paths.*~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/(workspace/\\\\{workspace_id\\\\}|workspaces|workspace$|workspace\\\\?|auth|user|organization|organizations|publishing-tokens|reports|suggest|schema_store|short_urls|artifacts|oci|subscriptions|github|code_sample)\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/speakeasy/refs/heads/main/rules/speakeasy-rules.yml
tags:
- AI
- Documentation
- MCP
- Platform
- SDKs
- Terraform
- Testing
- Spectral
- Linting
- API Governance
---
