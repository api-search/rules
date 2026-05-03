---
api_specs:
- filename: step-functions-openapi.yml
  format: yaml
  label: AWS Step Functions API
  slug: step-functions
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/step-functions/refs/heads/main/openapi/step-functions-openapi.yml
categories:
- step
description: Spectral linting rules defining API design standards and conventions for AWS Step Functions.
layout: rules
name: AWS Step Functions API Rules
provider_name: AWS Step Functions
provider_slug: step-functions
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: step-functions-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: step-functions-tags-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][*].operationId
  name: step-functions-operation-id-camel-case
  severity: warn
- description: All POST operations must return a 200 response
  given: $.paths[*].post
  name: step-functions-response-200-required
  severity: error
- description: AWS Step Functions API uses application/x-amz-json-1.0 content type
  given: $.paths[*][*].requestBody.content
  name: step-functions-content-type-json
  severity: warn
- description: All operations should define security requirements
  given: $.paths[*][*]
  name: step-functions-security-defined
  severity: warn
- description: All operations must have descriptions
  given: $.paths[*][*]
  name: step-functions-descriptions-required
  severity: error
- description: All parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: step-functions-parameters-described
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: step-functions-schemas-have-descriptions
  severity: info
rules_file: rules/step-functions-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/step-functions/refs/heads/main/rules/step-functions-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: step-functions-rules
source_filename: step-functions-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  step-functions-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  step-functions-tags-required:\n    description: All operations must have at least one tag\n    message: Operations must include tags for categorization\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  step-functions-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  step-functions-response-200-required:\n\
  \    description: All POST operations must return a 200 response\n    message: POST operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.200\n      function: truthy\n\n  step-functions-content-type-json:\n    description: AWS Step Functions API uses application/x-amz-json-1.0 content type\n    message: Request body should use application/x-amz-json-1.0 content type\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      field: \"application/x-amz-json-1.0\"\n      function: defined\n\n  step-functions-security-defined:\n    description: All operations should define security requirements\n    message: Operations should specify AWS SigV4 security\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  step-functions-descriptions-required:\n    description: All operations must have descriptions\n    message: Operations must include\
  \ descriptions\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  step-functions-parameters-described:\n    description: All parameters should have descriptions\n    message: \"Parameter is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  step-functions-schemas-have-descriptions:\n    description: Schema properties should have descriptions\n    message: Schema property should have a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/step-functions/refs/heads/main/rules/step-functions-rules.yml
tags:
- API Composition
- Serverless Orchestration
- Workflow
- State Machine
- Automation
- Spectral
- Linting
- API Governance
---
