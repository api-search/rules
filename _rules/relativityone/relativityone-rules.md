---
api_specs:
- filename: relativityone-legal-hold-openapi.yml
  format: yaml
  label: Legal Hold API
  slug: legal-hold-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/relativityone/refs/heads/main/openapi/relativityone-legal-hold-openapi.yml
categories:
- relativityone
description: Spectral linting rules defining API design standards and conventions for RelativityOne.
layout: rules
name: RelativityOne API Rules
provider_name: RelativityOne
provider_slug: relativityone
rule_count: 10
rules:
- description: All resource paths should include a workspaceId parameter to scope operations to a workspace.
  given: $.paths[*]
  name: relativityone-workspace-scoped-path
  severity: warn
- description: Path parameters named workspaceId, projectId, taskId, entityId should be integer type.
  given: $.paths[*][*].parameters[?(@.name =~ /Id$/ && @.in == 'path')].schema
  name: relativityone-integer-artifact-ids
  severity: warn
- description: All operations should have at least one tag for grouping in documentation.
  given: $.paths[*][*]
  name: relativityone-operation-tags
  severity: error
- description: All operations must have unique operationIds in camelCase.
  given: $.paths[*][*]
  name: relativityone-operation-ids
  severity: error
- description: OperationIds should use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: relativityone-operation-id-camel-case
  severity: warn
- description: Operation summaries should use Title Case.
  given: $.paths[*][*].summary
  name: relativityone-title-case-summaries
  severity: warn
- description: All response codes should have descriptions.
  given: $.paths[*][*].responses[*]
  name: relativityone-response-descriptions
  severity: warn
- description: Request bodies should use application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: relativityone-json-content-type
  severity: error
- description: Schema properties should have descriptions for API clarity.
  given: $.components.schemas[*].properties[*]
  name: relativityone-schema-descriptions
  severity: info
- description: GET operations returning lists should support start and length pagination parameters.
  given: $.paths[*].get
  name: relativityone-pagination-on-lists
  severity: info
rules_file: rules/relativityone-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/relativityone/refs/heads/main/rules/relativityone-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 5
slug: relativityone-rules
source_filename: relativityone-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # RelativityOne enforces workspace-scoped paths\n  relativityone-workspace-scoped-path:\n    description: All resource paths should include a workspaceId parameter to scope operations to a workspace.\n    message: \"Path '{{property}}' should include a workspaceId parameter for workspace scoping.\"\n    given: \"$.paths[*]\"\n    severity: warn\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \".*workspaces/\\\\{workspaceId\\\\}.*\"\n\n  # RelativityOne uses artifactId as integer identifiers\n  relativityone-integer-artifact-ids:\n    description: Path parameters named workspaceId, projectId, taskId, entityId should be integer type.\n    message: \"Path parameter '{{property}}' should have type integer in RelativityOne APIs.\"\n    given: \"$.paths[*][*].parameters[?(@.name =~ /Id$/ && @.in == 'path')].schema\"\n    severity: warn\n    then:\n      field: type\n      function: enumeration\n\
  \      functionOptions:\n        values:\n          - integer\n\n  # All operations must have tags\n  relativityone-operation-tags:\n    description: All operations should have at least one tag for grouping in documentation.\n    message: \"Operation '{{path}}' is missing tags.\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  # All operations must have operationIds\n  relativityone-operation-ids:\n    description: All operations must have unique operationIds in camelCase.\n    message: \"Operation '{{path}}' is missing an operationId.\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  # operationIds should be camelCase\n  relativityone-operation-id-camel-case:\n    description: OperationIds should use camelCase naming convention.\n    message: \"OperationId '{{value}}' should use camelCase.\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n \
  \   then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries should use Title Case\n  relativityone-title-case-summaries:\n    description: Operation summaries should use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # All responses should have descriptions\n  relativityone-response-descriptions:\n    description: All response codes should have descriptions.\n    message: \"Response '{{path}}' is missing a description.\"\n    given: \"$.paths[*][*].responses[*]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # POST/PUT request bodies should use application/json\n  relativityone-json-content-type:\n    description: Request bodies should use application/json content type.\n    message: \"\
  Request body at '{{path}}' should use application/json.\"\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    severity: error\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  # All schemas should have descriptions\n  relativityone-schema-descriptions:\n    description: Schema properties should have descriptions for API clarity.\n    message: \"Schema property '{{path}}' is missing a description.\"\n    given: \"$.components.schemas[*].properties[*]\"\n    severity: info\n    then:\n      field: description\n      function: truthy\n\n  # Collections should use pagination parameters\n  relativityone-pagination-on-lists:\n    description: GET operations returning lists should support start and length pagination parameters.\n    message: \"List operation '{{path}}' should support pagination via start and length query parameters.\"\n    given: \"$.paths[*].get\"\n    severity: info\n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                type: string\n                enum: [\"start\", \"length\", \"page\", \"limit\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/relativityone/refs/heads/main/rules/relativityone-rules.yml
tags:
- eDiscovery
- Legal
- Legal Hold
- Document Management
- Compliance
- Litigation
- Spectral
- Linting
- API Governance
---
