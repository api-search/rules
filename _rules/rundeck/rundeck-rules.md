---
api_specs:
- filename: rundeck-openapi.yml
  format: yaml
  label: Rundeck API
  slug: rundeck-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rundeck/refs/heads/main/openapi/rundeck-openapi.yml
categories:
- rundeck
description: Spectral linting rules defining API design standards and conventions for Rundeck.
layout: rules
name: Rundeck API Rules
provider_name: Rundeck
provider_slug: rundeck
rule_count: 18
rules:
- description: All operations must have an operationId for code generation
  given: $.paths[*][get,post,put,patch,delete]
  name: rundeck-operation-id-required
  severity: error
- description: Rundeck operationIds use camelCase convention (e.g., listJobs, runJob, getExecution). This ensures consistent client SDK method naming.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: rundeck-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: rundeck-tags-required
  severity: error
- description: Tags must use Title Case (e.g., "Jobs", "Executions", "Projects")
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: rundeck-tags-title-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: rundeck-summary-required
  severity: error
- description: Operation summaries must use Title Case (e.g., "List Jobs", "Run Job", "Get Execution Status"). This matches Rundeck's documentation style.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: rundeck-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: rundeck-description-required
  severity: warn
- description: Rundeck API requires authentication on all protected endpoints. Operations must document the 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: rundeck-responses-must-include-401
  severity: warn
- description: GET operations must define a 200 success response
  given: $.paths[*].get.responses
  name: rundeck-get-must-return-200
  severity: error
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: rundeck-delete-must-return-204
  severity: warn
- description: POST operations must return either 200 or 201
  given: $.paths[*].post.responses
  name: rundeck-post-must-return-200-or-201
  severity: warn
- description: Path operations containing {project} must have the project parameter documented. Rundeck organizes most resources under projects.
  given: $.paths[~/project/~][*].parameters[?(@.name == 'project')]
  name: rundeck-project-path-parameter
  severity: error
- description: Path operations with {id} for executions must mark id as required
  given: $.paths[~/execution/~][*].parameters[?(@.name == 'id')]
  name: rundeck-execution-id-path-parameter
  severity: error
- description: Rundeck uses X-Rundeck-Auth-Token header for API token authentication. Security schemes should reference this header name.
  given: $.components.securitySchemes[?(@.type == 'apiKey')].name
  name: rundeck-token-auth-header-name
  severity: warn
- description: All schema properties should have a type defined
  given: $.components.schemas[*].properties[*]
  name: rundeck-schema-type-required
  severity: warn
- description: API responses should use application/json content type
  given: $.paths[*][get,post,put].responses[200,201].content
  name: rundeck-response-content-type-json
  severity: warn
- description: API info must include contact information
  given: $.info
  name: rundeck-info-contact-required
  severity: warn
- description: At least one server must be defined
  given: $
  name: rundeck-servers-defined
  severity: error
rules_file: rules/rundeck-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rundeck/refs/heads/main/rules/rundeck-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 11
slug: rundeck-rules
source_filename: rundeck-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Rundeck API conventions: all paths under /api/N/ versioning\n  rundeck-operation-id-required:\n    description: All operations must have an operationId for code generation\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  rundeck-operation-id-camel-case:\n    description: >-\n      Rundeck operationIds use camelCase convention (e.g., listJobs, runJob,\n      getExecution). This ensures consistent client SDK method naming.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  rundeck-tags-required:\n    description: All operations must have at least one tag for grouping\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  rundeck-tags-title-case:\n\
  \    description: Tags must use Title Case (e.g., \"Jobs\", \"Executions\", \"Projects\")\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  rundeck-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  rundeck-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case (e.g., \"List Jobs\", \"Run Job\",\n      \"Get Execution Status\"). This matches Rundeck's documentation style.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  rundeck-description-required:\n    description: All operations must have a description\n    severity: warn\n   \
  \ given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  rundeck-responses-must-include-401:\n    description: >-\n      Rundeck API requires authentication on all protected endpoints.\n      Operations must document the 401 Unauthorized response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  rundeck-get-must-return-200:\n    description: GET operations must define a 200 success response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  rundeck-delete-must-return-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  rundeck-post-must-return-200-or-201:\n    description: POST operations must return either 200 or 201\n\
  \    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  rundeck-project-path-parameter:\n    description: >-\n      Path operations containing {project} must have the project parameter documented.\n      Rundeck organizes most resources under projects.\n    severity: error\n    given: \"$.paths[~/project/~][*].parameters[?(@.name == 'project')]\"\n    then:\n      field: required\n      function: truthy\n\n  rundeck-execution-id-path-parameter:\n    description: Path operations with {id} for executions must mark id as required\n    severity: error\n    given: \"$.paths[~/execution/~][*].parameters[?(@.name == 'id')]\"\n    then:\n      field: required\n      function: truthy\n\n  rundeck-token-auth-header-name:\n    description: >-\n      Rundeck uses X-Rundeck-Auth-Token header for API token authentication.\n   \
  \   Security schemes should reference this header name.\n    severity: warn\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^X-Rundeck-Auth-Token$\"\n\n  rundeck-schema-type-required:\n    description: All schema properties should have a type defined\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  rundeck-response-content-type-json:\n    description: API responses should use application/json content type\n    severity: warn\n    given: \"$.paths[*][get,post,put].responses[200,201].content\"\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  rundeck-info-contact-required:\n    description: API info must include contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  rundeck-servers-defined:\n    description: At\
  \ least one server must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rundeck/refs/heads/main/rules/rundeck-rules.yml
tags:
- Automation
- DevOps
- Job Scheduling
- Orchestration
- Workflow
- Runbook
- Open Source
- IT Operations
- Spectral
- Linting
- API Governance
---
