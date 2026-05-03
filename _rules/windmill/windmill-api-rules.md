---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Windmill API
  slug: windmill-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/windmill-labs/windmill/main/backend/windmill-api/openapi.yaml
categories:
- windmill
description: Spectral linting rules defining API design standards and conventions for Windmill.
layout: rules
name: Windmill API Rules
provider_name: Windmill
provider_slug: windmill
rule_count: 10
rules:
- description: Workspace-scoped paths must use /w/{workspace}/ prefix
  given: $.paths
  name: windmill-workspace-path-prefix
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: windmill-path-kebab-case
  severity: warn
- description: OperationIds should use camelCase per Windmill convention
  given: $.paths[*][*].operationId
  name: windmill-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: windmill-operation-tags-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: windmill-summary-required
  severity: error
- description: Operations must define at least one success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: windmill-success-response-required
  severity: error
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: windmill-schema-descriptions
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: windmill-parameter-descriptions
  severity: warn
- description: Workspace path parameter must be named 'workspace'
  given: $.paths['/w/{workspace}/**'][*].parameters[?(@.in=='path')]
  name: windmill-workspace-param-name
  severity: warn
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: windmill-no-get-request-body
  severity: error
rules_file: rules/windmill-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/windmill/refs/heads/main/rules/windmill-api-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: windmill-api-rules
source_filename: windmill-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Windmill uses workspace-scoped paths: /w/{workspace}/{resource}\n  windmill-workspace-path-prefix:\n    description: Workspace-scoped paths must use /w/{workspace}/ prefix\n    message: \"Workspace operations should use '/w/{workspace}/' path prefix, got: {{value}}\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # All paths should use kebab-case segments\n  windmill-path-kebab-case:\n    description: Path segments should use kebab-case\n    message: \"Path segment '{{value}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_\\\\-]+)+$\"\n\n  # All operation IDs should use camelCase (Windmill convention)\n  windmill-operation-id-camel-case:\n    description: OperationIds should use camelCase per Windmill convention\n\
  \    message: \"OperationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Operations must have tags\n  windmill-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summaries must be present\n  windmill-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Windmill uses 200 for success; all successful responses must be documented\n  windmill-success-response-required:\n    description: Operations must define at least one\
  \ success response\n    message: \"Operation has no success (2xx) response defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  # Schemas should have descriptions\n  windmill-schema-descriptions:\n    description: Schema components should have descriptions\n    message: \"Schema component '{{path}}' is missing a description\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Parameters should have descriptions\n  windmill-parameter-descriptions:\n    description: Parameters should have descriptions\n    message: \"Parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Workspace path parameter must be named 'workspace'\n\
  \  windmill-workspace-param-name:\n    description: Workspace path parameter must be named 'workspace'\n    message: \"Workspace path parameter should be named 'workspace', not '{{value}}'\"\n    severity: warn\n    given: \"$.paths['/w/{workspace}/**'][*].parameters[?(@.in=='path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - workspace\n\n  # GET operations must not have request bodies\n  windmill-no-get-request-body:\n    description: GET operations must not have request bodies\n    message: \"GET operation should not have a requestBody\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/windmill/refs/heads/main/rules/windmill-api-rules.yml
tags:
- Automation
- Internal Tools
- Open Source
- ProCode API Composition
- Scripts
- Webhooks
- Workflow Engine
- Workflows
- Spectral
- Linting
- API Governance
---
