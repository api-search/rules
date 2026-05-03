---
api_specs:
- filename: openapi.json
  format: json
  label: Robocorp Control Room API
  slug: control-room-api
  spec_type: OpenAPI
  url: https://robocorp.com/api/openapi.json
categories:
- robocorp
description: Spectral linting rules defining API design standards and conventions for Robocorp.
layout: rules
name: Robocorp API Rules
provider_name: Robocorp
provider_slug: robocorp
rule_count: 13
rules:
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: robocorp-operation-has-tag
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: robocorp-operation-has-summary
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: robocorp-operation-has-description
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: robocorp-operation-has-operation-id
  severity: error
- description: All resource paths should include workspace_id
  given: $.paths[*]~
  name: robocorp-workspace-id-in-path
  severity: warn
- description: Control Room API uses RC-WSKEY prefixed API keys
  given: $.components.securitySchemes[*]
  name: robocorp-rc-wskey-auth
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: robocorp-delete-returns-204
  severity: warn
- description: POST operations that create resources should return 201
  given: $.paths[*].post
  name: robocorp-post-create-returns-201
  severity: info
- description: List operations should support pagination with cursor
  given: $.paths[*].get
  name: robocorp-list-operations-paginated
  severity: info
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: robocorp-camel-case-operation-id
  severity: warn
- description: State fields should use defined enumerations
  given: $.components.schemas[*].properties.state
  name: robocorp-state-enum-defined
  severity: info
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: robocorp-schema-has-description
  severity: info
- description: Operations should define 401 unauthorized response
  given: $.paths[*][get,post,put,patch,delete]
  name: robocorp-has-error-response
  severity: warn
rules_file: rules/robocorp-control-room-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/robocorp/refs/heads/main/rules/robocorp-control-room-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 7
slug: robocorp-control-room-rules
source_filename: robocorp-control-room-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Robocorp Control Room API Conventions\n\n  robocorp-operation-has-tag:\n    description: All operations must have at least one tag\n    message: Operation {{path}} is missing a tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  robocorp-operation-has-summary:\n    description: All operations must have a summary\n    message: Operation {{path}} is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  robocorp-operation-has-description:\n    description: All operations should have a description\n    message: Operation {{path}} should include a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  robocorp-operation-has-operation-id:\n    description: All operations\
  \ must have an operationId\n    message: Operation {{path}} is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  robocorp-workspace-id-in-path:\n    description: All resource paths should include workspace_id\n    message: Path {{path}} should include workspace_id parameter\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/workspaces/\\\\{workspace_id\\\\}/\"\n\n  robocorp-rc-wskey-auth:\n    description: Control Room API uses RC-WSKEY prefixed API keys\n    message: Security scheme should use apiKey with Authorization header\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              type: string\n              enum:\n               \
  \ - apiKey\n\n  robocorp-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: DELETE operation {{path}} should return 204\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: truthy\n\n  robocorp-post-create-returns-201:\n    description: POST operations that create resources should return 201\n    message: POST create operation {{path}} should return 201\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      field: responses\n      function: truthy\n\n  robocorp-list-operations-paginated:\n    description: List operations should support pagination with cursor\n    message: List operation {{path}} should support cursor-based pagination\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  robocorp-camel-case-operation-id:\n    description: OperationIds should use camelCase\n    message: OperationId {{value}}\
  \ should use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  robocorp-state-enum-defined:\n    description: State fields should use defined enumerations\n    message: State property {{path}} should define allowed values\n    severity: info\n    given: \"$.components.schemas[*].properties.state\"\n    then:\n      field: enum\n      function: truthy\n\n  robocorp-schema-has-description:\n    description: Schema components should have descriptions\n    message: Schema {{path}} is missing a description\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  robocorp-has-error-response:\n    description: Operations should define 401 unauthorized response\n    message: Operation {{path}} should define 401 response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: responses.401\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/robocorp/refs/heads/main/rules/robocorp-control-room-rules.yml
tags:
- RPA
- Workflow Automation
- Python
- Open Source
- Automation
- Spectral
- Linting
- API Governance
---
