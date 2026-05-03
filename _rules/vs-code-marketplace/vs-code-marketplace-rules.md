---
api_specs:
- filename: vs-code-marketplace-gallery-api-openapi.yml
  format: yaml
  label: VS Code Marketplace Gallery API
  slug: vs-code-marketplace-gallery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vs-code-marketplace/refs/heads/main/openapi/vs-code-marketplace-gallery-api-openapi.yml
categories:
- vscode
description: Spectral linting rules defining API design standards and conventions for VS Code Marketplace.
layout: rules
name: VS Code Marketplace API Rules
provider_name: VS Code Marketplace
provider_slug: vs-code-marketplace
rule_count: 9
rules:
- description: Operation IDs must use camelCase.
  given: $.paths[*][*].operationId
  name: vscode-marketplace-operation-ids-camel-case
  severity: warn
- description: Tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: vscode-marketplace-tags-title-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: vscode-marketplace-operation-summary-required
  severity: error
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: vscode-marketplace-operation-description-required
  severity: info
- description: POST operations must define a request body.
  given: $.paths[*].post
  name: vscode-marketplace-post-has-request-body
  severity: error
- description: GET and POST operations must define a 200 response.
  given: $.paths[*][get,post]
  name: vscode-marketplace-response-200-or-202
  severity: warn
- description: Marketplace Gallery API endpoints require an api-version query parameter.
  given: $.paths[*][post,get].parameters[*]
  name: vscode-marketplace-api-version-query-param
  severity: info
- description: API path segments should be lowercase.
  given: $.paths
  name: vscode-marketplace-path-lowercase
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: vscode-marketplace-schema-descriptions
  severity: info
rules_file: rules/vs-code-marketplace-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vs-code-marketplace/refs/heads/main/rules/vs-code-marketplace-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 4
slug: vs-code-marketplace-rules
source_filename: vs-code-marketplace-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vscode-marketplace-operation-ids-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vscode-marketplace-tags-title-case:\n    description: Tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 \\\\-]*$\"\n\n  vscode-marketplace-operation-summary-required:\n    description: All operations must have a summary.\n    message: \"Operation must have a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  vscode-marketplace-operation-description-required:\n\
  \    description: All operations should have a description.\n    message: \"Operation should have a description.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: defined\n\n  vscode-marketplace-post-has-request-body:\n    description: POST operations must define a request body.\n    message: \"POST operation must define a requestBody.\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  vscode-marketplace-response-200-or-202:\n    description: GET and POST operations must define a 200 response.\n    message: \"GET/POST operation must define a 200 response.\"\n    severity: warn\n    given: \"$.paths[*][get,post]\"\n    then:\n      field: responses.200\n      function: defined\n\n  vscode-marketplace-api-version-query-param:\n    description: >-\n      Marketplace Gallery API endpoints require an api-version query parameter.\n    message:\
  \ \"Marketplace API operations should document the api-version parameter.\"\n    severity: info\n    given: \"$.paths[*][post,get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            name:\n              type: string\n\n  vscode-marketplace-path-lowercase:\n    description: API path segments should be lowercase.\n    message: \"Path '{{path}}' should use lowercase segments.\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}\\\\-._~]*)*$\"\n\n  vscode-marketplace-schema-descriptions:\n    description: Schema properties should have descriptions.\n    message: \"Schema property should have a description.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vs-code-marketplace/refs/heads/main/rules/vs-code-marketplace-rules.yml
tags:
- Developer Tools
- Extensions
- IDE
- Microsoft
- Spectral
- Linting
- API Governance
---
