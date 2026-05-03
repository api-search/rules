---
api_specs:
- filename: openapi.json
  format: json
  label: Einstein Vision API
  slug: ''
  spec_type: OpenAPI
  url: https://api.einstein.ai/v2/vision/openapi.json
- filename: openapi.json
  format: json
  label: Einstein Language API
  slug: ''
  spec_type: OpenAPI
  url: https://api.einstein.ai/v2/language/openapi.json
- filename: salesforce-einstein-prediction-builder-openapi.yml
  format: yaml
  label: Einstein Prediction Builder API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/openapi/salesforce-einstein-prediction-builder-openapi.yml
- filename: salesforce-einstein-discovery-openapi.yml
  format: yaml
  label: Einstein Discovery API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/openapi/salesforce-einstein-discovery-openapi.yml
- filename: salesforce-einstein-bots-openapi.yml
  format: yaml
  label: Einstein Bots API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/openapi/salesforce-einstein-bots-openapi.yml
- filename: salesforce-einstein-gpt-openapi.yml
  format: yaml
  label: Einstein GPT API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/openapi/salesforce-einstein-gpt-openapi.yml
categories:
- einstein
description: Spectral linting rules defining API design standards and conventions for Salesforce Einstein.
layout: rules
name: Salesforce Einstein API Rules
provider_name: Salesforce Einstein
provider_slug: salesforce-einstein
rule_count: 9
rules:
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: einstein-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: einstein-summary-not-empty
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: einstein-tags-required
  severity: warn
- description: All operations must define a 200 success response.
  given: $.paths[*][*].responses
  name: einstein-response-200-required
  severity: error
- description: All Einstein APIs require bearer token or OAuth2.
  given: $.components.securitySchemes
  name: einstein-auth-required
  severity: error
- description: API must define at least one server URL.
  given: $
  name: einstein-server-url-defined
  severity: error
- description: JSON request bodies must use application/json.
  given: $.paths[*][*].requestBody.content
  name: einstein-content-type-json
  severity: warn
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: einstein-no-trailing-slash
  severity: error
- description: API info must include a description.
  given: $.info
  name: einstein-description-required
  severity: warn
rules_file: rules/salesforce-einstein-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/rules/salesforce-einstein-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 3
slug: salesforce-einstein-rules
source_filename: salesforce-einstein-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  einstein-operation-id-required:\n    description: All operations must have an operationId.\n    message: \"Operation is missing operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  einstein-summary-not-empty:\n    description: All operations must have a summary.\n    message: \"Operation must have a non-empty summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  einstein-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  einstein-response-200-required:\n    description: All operations must define a 200 success response.\n    message: \"Operation must define a 200 success response.\"\n    severity: error\n \
  \   given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n\n  einstein-auth-required:\n    description: All Einstein APIs require bearer token or OAuth2.\n    message: \"API must declare bearer or OAuth2 security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"bearerAuth\"]\n            - required: [\"oauth2\"]\n\n  einstein-server-url-defined:\n    description: API must define at least one server URL.\n    message: \"API must define at least one server.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  einstein-content-type-json:\n    description: JSON request bodies must use application/json.\n    message: \"JSON request body should declare application/json.\"\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"application/json\"]\n            - required: [\"multipart/form-data\"]\n\n  einstein-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n    message: \"Path must not end with a slash.\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  einstein-description-required:\n    description: API info must include a description.\n    message: \"API info must include a description.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-einstein/refs/heads/main/rules/salesforce-einstein-rules.yml
tags:
- Artificial Intelligence
- Computer Vision
- CRM
- Machine Learning
- Natural Language Processing
- Predictive Analytics
- Salesforce
- Spectral
- Linting
- API Governance
---
