---
api_specs:
- filename: tensorflow-serving-openapi.yml
  format: yaml
  label: TensorFlow Serving REST API
  slug: tensorflow-serving-rest
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tensorflow/refs/heads/main/openapi/tensorflow-serving-openapi.yml
categories:
- tensorflow
description: Spectral linting rules defining API design standards and conventions for TensorFlow.
layout: rules
name: TensorFlow API Rules
provider_name: TensorFlow
provider_slug: tensorflow
rule_count: 13
rules:
- description: Operation IDs should use camelCase following TensorFlow Serving conventions
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: tensorflow-operation-id-kebab-case
  severity: warn
- description: Model endpoints must include model_name path parameter
  given: $.paths['/v1/models/{model_name}*']
  name: tensorflow-model-name-in-path
  severity: false
- description: All TensorFlow Serving API paths must be versioned with /v1/
  given: $.paths[*]~
  name: tensorflow-path-versioned
  severity: error
- description: Inference endpoints (classify, regress, predict) must use POST
  given: $.paths[*classify,*regress,*predict]
  name: tensorflow-inference-methods
  severity: error
- description: Model status and metadata endpoints must use GET
  given: $.paths['/v1/models/{model_name}','/v1/models/{model_name}/metadata']
  name: tensorflow-status-get-method
  severity: error
- description: All operations must define a 200 success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tensorflow-response-200-defined
  severity: error
- description: Operations should define error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tensorflow-error-response-defined
  severity: warn
- description: Inference operations must define a request body
  given: $.paths[*classify,*regress,*predict].post
  name: tensorflow-request-body-inference
  severity: error
- description: TensorFlow Serving uses JSON for all request/response bodies
  given: $.paths[*][post].requestBody.content
  name: tensorflow-json-content-type
  severity: warn
- description: All operations should be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: tensorflow-tags-defined
  severity: warn
- description: All operation summaries should use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tensorflow-summary-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: tensorflow-description-present
  severity: warn
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: tensorflow-schema-descriptions
  severity: warn
rules_file: rules/tensorflow-serving-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tensorflow/refs/heads/main/rules/tensorflow-serving-rules.yml
severity_counts:
  error: 5
  warn: 7
  info: 0
  hint: 0
  false: 1
slug: tensorflow-serving-rules
source_filename: tensorflow-serving-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Naming Conventions\n  tensorflow-operation-id-kebab-case:\n    description: Operation IDs should use camelCase following TensorFlow Serving conventions\n    message: \"Operation ID '{{value}}' should use camelCase\"\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n    severity: warn\n\n  tensorflow-model-name-in-path:\n    description: Model endpoints must include model_name path parameter\n    message: \"Model inference paths should include {model_name} path parameter\"\n    given: \"$.paths['/v1/models/{model_name}*']\"\n    then:\n      field: get\n      function: truthy\n    severity: off\n\n  tensorflow-path-versioned:\n    description: All TensorFlow Serving API paths must be versioned with /v1/\n    message: \"Path '{{property}}' must start with /v1/\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^/v1/\"\n    severity: error\n\n  tensorflow-inference-methods:\n    description: Inference endpoints (classify, regress, predict) must use POST\n    message: \"TensorFlow Serving inference endpoints must use POST method\"\n    given: \"$.paths[*classify,*regress,*predict]\"\n    then:\n      field: post\n      function: truthy\n    severity: error\n\n  tensorflow-status-get-method:\n    description: Model status and metadata endpoints must use GET\n    message: \"Model status and metadata endpoints must use GET method\"\n    given: \"$.paths['/v1/models/{model_name}','/v1/models/{model_name}/metadata']\"\n    then:\n      field: get\n      function: truthy\n    severity: error\n\n  tensorflow-response-200-defined:\n    description: All operations must define a 200 success response\n    message: \"Operation '{{path}}' must define a 200 success response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"\
  200\"\n      function: truthy\n    severity: error\n\n  tensorflow-error-response-defined:\n    description: Operations should define error responses\n    message: \"Operation should define at least one error response (4xx)\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['400']\n            - required: ['401']\n            - required: ['404']\n    severity: warn\n\n  tensorflow-request-body-inference:\n    description: Inference operations must define a request body\n    message: \"Inference operation '{{path}}' must define a request body\"\n    given: \"$.paths[*classify,*regress,*predict].post\"\n    then:\n      field: requestBody\n      function: truthy\n    severity: error\n\n  tensorflow-json-content-type:\n    description: TensorFlow Serving uses JSON for all request/response bodies\n    message: \"TensorFlow Serving endpoints should use application/json\
  \ content type\"\n    given: \"$.paths[*][post].requestBody.content\"\n    then:\n      field: \"application/json\"\n      function: truthy\n    severity: warn\n\n  tensorflow-tags-defined:\n    description: All operations should be tagged\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  tensorflow-summary-title-case:\n    description: All operation summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n    severity: warn\n\n  tensorflow-description-present:\n    description: All operations should have a description\n    message: \"Operation is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\
  \    severity: warn\n\n  tensorflow-schema-descriptions:\n    description: Schema components should have descriptions\n    message: \"Schema '{{path}}' is missing a description\"\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tensorflow/refs/heads/main/rules/tensorflow-serving-rules.yml
tags:
- AI
- Deep Learning
- JavaScript
- Machine Learning
- Model Serving
- Neural Networks
- Open Source
- Python
- Spectral
- Linting
- API Governance
---
