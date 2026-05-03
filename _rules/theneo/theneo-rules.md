---
api_specs:
- filename: theneo-api-openapi.yml
  format: yaml
  label: Theneo
  slug: theneo
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/theneo/refs/heads/main/openapi/theneo-api-openapi.yml
categories:
- theneo
description: Spectral linting rules defining API design standards and conventions for Theneo.
layout: rules
name: Theneo API Rules
provider_name: Theneo
provider_slug: theneo
rule_count: 10
rules:
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: theneo-operation-ids-camel-case
  severity: warn
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: theneo-operation-summary-title-case
  severity: warn
- description: All path segments must use kebab-case.
  given: $.paths[*]~
  name: theneo-path-kebab-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: theneo-tags-required
  severity: error
- description: All operations must declare the apiKey security scheme.
  given: $.paths[*][get,post,put,patch,delete]
  name: theneo-api-key-security
  severity: warn
- description: All operations must define a 401 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: theneo-responses-401-defined
  severity: warn
- description: POST/PUT/PATCH request bodies must declare application/json or multipart/form-data content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: theneo-request-body-content-type
  severity: warn
- description: Paths with {projectId} must document the parameter in-path with required=true.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'projectId')]
  name: theneo-project-id-path-param
  severity: error
- description: All operations must have a non-empty description.
  given: $.paths[*][get,post,put,patch,delete]
  name: theneo-no-empty-descriptions
  severity: warn
- description: All 200/201 responses must define a schema.
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content
  name: theneo-response-schema-defined
  severity: warn
rules_file: rules/theneo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/theneo/refs/heads/main/rules/theneo-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 8
slug: theneo-rules
source_filename: theneo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  theneo-operation-ids-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  theneo-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  theneo-path-kebab-case:\n    description: All path segments must use kebab-case.\n    message: \"Path '{{path}}' must use kebab-case segments.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{][a-z0-9-{}]*)*$\"\n\n  theneo-tags-required:\n\
  \    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  theneo-api-key-security:\n    description: All operations must declare the apiKey security scheme.\n    message: \"Operation at '{{path}}' should declare apiKey security.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  theneo-responses-401-defined:\n    description: All operations must define a 401 response.\n    message: \"Operation at '{{path}}' must define a 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  theneo-request-body-content-type:\n    description: POST/PUT/PATCH\
  \ request bodies must declare application/json or multipart/form-data content type.\n    message: \"Request body at '{{path}}' must declare an explicit content type.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: truthy\n\n  theneo-project-id-path-param:\n    description: Paths with {projectId} must document the parameter in-path with required=true.\n    message: \"Parameter 'projectId' must be required=true in '{{path}}'.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'projectId')]\"\n    then:\n      field: required\n      function: truthy\n\n  theneo-no-empty-descriptions:\n    description: All operations must have a non-empty description.\n    message: \"Operation at '{{path}}' must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  theneo-response-schema-defined:\n\
  \    description: All 200/201 responses must define a schema.\n    message: \"Response at '{{path}}' must define a content schema.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/theneo/refs/heads/main/rules/theneo-rules.yml
tags:
- API Documentation
- Developer Tools
- Documentation Platform
- AI
- Platform
- Spectral
- Linting
- API Governance
---
