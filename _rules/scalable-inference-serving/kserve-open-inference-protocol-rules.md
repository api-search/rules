---
api_specs:
- filename: kserve-open-inference-protocol-openapi.yml
  format: yaml
  label: KServe Open Inference Protocol API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/openapi/kserve-open-inference-protocol-openapi.yml
categories:
- oip
description: Spectral linting rules defining API design standards and conventions for Scalable Inference Serving.
layout: rules
name: Scalable Inference Serving API Rules
provider_name: Scalable Inference Serving
provider_slug: scalable-inference-serving
rule_count: 17
rules:
- description: All Open Inference Protocol paths must start with /v2/
  given: $.paths[*]~
  name: oip-v2-prefix
  severity: error
- description: Health endpoints must use /v2/health/{live|ready} naming convention
  given: $.paths[?(@property.match(/health/))]~
  name: oip-health-paths-standard
  severity: warn
- description: Model paths must use /v2/models/{model_name} naming convention
  given: $.paths[?(@property.match(/models/))]~
  name: oip-model-path-convention
  severity: warn
- description: Inference endpoints must use HTTP POST
  given: $.paths[?(@property.match(/\/infer$/))]
  name: oip-inference-post-only
  severity: error
- description: Operation IDs should use PascalCase (e.g., RunInference, GetModelMetadata)
  given: $.paths[*][*].operationId
  name: oip-operation-ids-pascal-case
  severity: warn
- description: Inference 200 responses must include model_name in the response schema
  given: $.paths[?(@property.match(/infer/))].post.responses['200'].content['application/json'].schema
  name: oip-inference-response-has-model-name
  severity: warn
- description: Error responses must include an 'error' field in the response schema
  given: $.components.schemas.ErrorResponse.properties
  name: oip-error-response-has-error-field
  severity: error
- description: TensorDatatype must enumerate all OIP-defined data types
  given: $.components.schemas.TensorDatatype
  name: oip-tensor-datatype-enum
  severity: warn
- description: Inference request bodies must define an 'inputs' required field
  given: $.components.schemas.InferenceRequest.required
  name: oip-inference-request-has-inputs
  severity: error
- description: RequestInput must require name, shape, datatype, and data
  given: $.components.schemas.RequestInput.required
  name: oip-tensor-input-required-fields
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: oip-operations-tagged
  severity: warn
- description: All tags in the info and operation tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: oip-tags-title-case
  severity: info
- description: All operations must have a summary for Swagger UI display
  given: $.paths[*][get,post,put,patch,delete]
  name: oip-operations-have-summaries
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: oip-summaries-title-case
  severity: warn
- description: All component schemas should have a description
  given: $.components.schemas[*]
  name: oip-schemas-have-descriptions
  severity: info
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: oip-properties-have-descriptions
  severity: info
- description: At least one server must be defined
  given: $
  name: oip-servers-defined
  severity: warn
rules_file: rules/kserve-open-inference-protocol-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/rules/kserve-open-inference-protocol-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 3
  warn: 9
slug: kserve-open-inference-protocol-rules
source_filename: kserve-open-inference-protocol-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Path structure rules based on Open Inference Protocol conventions\n  oip-v2-prefix:\n    description: All Open Inference Protocol paths must start with /v2/\n    message: \"OIP paths must start with /v2/ — found: {{value}}\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2\"\n\n  oip-health-paths-standard:\n    description: Health endpoints must use /v2/health/{live|ready} naming convention\n    message: \"Health endpoints must follow /v2/health/live or /v2/health/ready pattern\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/health/))]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2/health/(live|ready)$\"\n\n  oip-model-path-convention:\n    description: Model paths must use /v2/models/{model_name} naming convention\n    message: \"Model paths should follow /v2/models/{model_name} pattern\"\n    severity:\
  \ warn\n    given: \"$.paths[?(@property.match(/models/))]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2/models/\\\\{model_name\\\\}\"\n\n  oip-inference-post-only:\n    description: Inference endpoints must use HTTP POST\n    message: \"Inference endpoints (/infer) must use HTTP POST method, not {{value}}\"\n    severity: error\n    given: \"$.paths[?(@property.match(/\\\\/infer$/))]\"\n    then:\n      field: post\n      function: defined\n\n  # Operation ID conventions\n  oip-operation-ids-pascal-case:\n    description: Operation IDs should use PascalCase (e.g., RunInference, GetModelMetadata)\n    message: \"OperationId '{{value}}' should use PascalCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]+$\"\n\n  # Response schema rules\n  oip-inference-response-has-model-name:\n    description: Inference 200 responses must include model_name\
  \ in the response schema\n    message: \"Inference response schema should include model_name property\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/infer/))].post.responses['200'].content['application/json'].schema\"\n    then:\n      field: \"$ref\"\n      function: defined\n\n  oip-error-response-has-error-field:\n    description: Error responses must include an 'error' field in the response schema\n    message: \"Error response schema must include the 'error' property\"\n    severity: error\n    given: \"$.components.schemas.ErrorResponse.properties\"\n    then:\n      field: error\n      function: defined\n\n  # Tensor data type validation\n  oip-tensor-datatype-enum:\n    description: TensorDatatype must enumerate all OIP-defined data types\n    message: \"TensorDatatype should include all OIP standard data types\"\n    severity: warn\n    given: \"$.components.schemas.TensorDatatype\"\n    then:\n      field: enum\n      function: defined\n\n  # Request body requirements\n\
  \  oip-inference-request-has-inputs:\n    description: Inference request bodies must define an 'inputs' required field\n    message: \"InferenceRequest schema must have 'inputs' in required array\"\n    severity: error\n    given: \"$.components.schemas.InferenceRequest.required\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - inputs\n\n  oip-tensor-input-required-fields:\n    description: RequestInput must require name, shape, datatype, and data\n    message: \"RequestInput should require: name, shape, datatype, data\"\n    severity: error\n    given: \"$.components.schemas.RequestInput.required\"\n    then:\n      function: defined\n\n  # Tag conventions\n  oip-operations-tagged:\n    description: All operations must have at least one tag\n    message: \"Operation '{{path}}' must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  oip-tags-title-case:\n\
  \    description: All tags in the info and operation tags must use Title Case\n    message: \"Tag '{{value}}' should use Title Case\"\n    severity: info\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &/()-]+$\"\n\n  # Summary quality rules\n  oip-operations-have-summaries:\n    description: All operations must have a summary for Swagger UI display\n    message: \"Operation in {{path}} is missing a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  oip-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 &/()-]+$\"\n\n  # Schema documentation rules\n  oip-schemas-have-descriptions:\n\
  \    description: All component schemas should have a description\n    message: \"Schema '{{path}}' is missing a description\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: defined\n\n  oip-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    message: \"Property at '{{path}}' is missing a description\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: defined\n\n  # Security\n  oip-servers-defined:\n    description: At least one server must be defined\n    message: \"No servers defined in the spec\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/rules/kserve-open-inference-protocol-rules.yml
tags:
- AI
- CNCF
- Deployment
- Inference
- Kubernetes
- LLM
- Machine Learning
- Model Serving
- MLOps
- Scalability
- Spectral
- Linting
- API Governance
---
