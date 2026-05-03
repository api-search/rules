---
api_specs:
- filename: stability-ai-stable-image-generate-openapi.yml
  format: yaml
  label: Stability AI Stable Image Generate API
  slug: stable-image-generate
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-image-generate-openapi.yml
- filename: stability-ai-stable-image-edit-openapi.yml
  format: yaml
  label: Stability AI Stable Image Edit API
  slug: stable-image-edit
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-image-edit-openapi.yml
- filename: stability-ai-stable-image-upscale-openapi.yml
  format: yaml
  label: Stability AI Stable Image Upscale API
  slug: stable-image-upscale
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-image-upscale-openapi.yml
- filename: stability-ai-stable-image-control-openapi.yml
  format: yaml
  label: Stability AI Stable Image Control API
  slug: stable-image-control
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-image-control-openapi.yml
- filename: stability-ai-stable-video-diffusion-openapi.yml
  format: yaml
  label: Stability AI Stable Video Diffusion API
  slug: stable-video-diffusion
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-video-diffusion-openapi.yml
- filename: stability-ai-stable-fast-3d-openapi.yml
  format: yaml
  label: Stability AI Stable Fast 3D API
  slug: stable-fast-3d
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/openapi/stability-ai-stable-fast-3d-openapi.yml
categories:
- stability
description: Spectral linting rules defining API design standards and conventions for Stability AI.
layout: rules
name: Stability AI API Rules
provider_name: Stability AI
provider_slug: stability-ai
rule_count: 10
rules:
- description: All Stability AI API operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: stability-ai-operation-summaries-title-case
  severity: warn
- description: All Stability AI API operations must require bearer authentication
  given: $.components.securitySchemes
  name: stability-ai-bearer-auth-required
  severity: error
- description: Stability AI image operations should use multipart/form-data request bodies
  given: $.paths[*].post.requestBody.content
  name: stability-ai-multipart-form-data
  severity: warn
- description: Stability AI API paths should use the /v2beta prefix
  given: $.paths[*]~
  name: stability-ai-v2beta-paths
  severity: warn
- description: Stability AI operationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: stability-ai-operationid-camel-case
  severity: warn
- description: All Stability AI API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: stability-ai-operations-must-have-operationid
  severity: error
- description: Stability AI API operations must define 400 and 401 error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: stability-ai-error-responses
  severity: warn
- description: Stability AI image generation requests should support output_format parameter
  given: $.components.schemas[*].properties
  name: stability-ai-output-format-parameter
  severity: warn
- description: Stability AI image generation responses should support binary image output
  given: $.paths[*].post.responses.200.content
  name: stability-ai-response-supports-binary
  severity: warn
- description: Stability AI generation requests should support a seed parameter for reproducibility
  given: $.components.schemas[*].properties
  name: stability-ai-seed-parameter
  severity: info
rules_file: rules/stability-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/rules/stability-ai-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: stability-ai-rules
source_filename: stability-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stability-ai-operation-summaries-title-case:\n    description: All Stability AI API operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  stability-ai-bearer-auth-required:\n    description: All Stability AI API operations must require bearer authentication\n    message: \"Stability AI API operations must use bearerAuth security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  stability-ai-multipart-form-data:\n    description: Stability AI image operations should use multipart/form-data request bodies\n    message: \"Image generation/editing operations should use multipart/form-data encoding\"\
  \n    severity: warn\n    given: \"$.paths[*].post.requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  stability-ai-v2beta-paths:\n    description: Stability AI API paths should use the /v2beta prefix\n    message: \"Path '{{value}}' should start with /v2beta\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2beta/\"\n\n  stability-ai-operationid-camel-case:\n    description: Stability AI operationIds must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stability-ai-operations-must-have-operationid:\n    description: All Stability AI API operations must have an operationId\n    message: \"Operation\
  \ is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  stability-ai-error-responses:\n    description: Stability AI API operations must define 400 and 401 error responses\n    message: \"Operation should define 400 and 401 error responses\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '400'\n            - '401'\n\n  stability-ai-output-format-parameter:\n    description: Stability AI image generation requests should support output_format parameter\n    message: \"Image request schema should include output_format property\"\n    severity: warn\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stability-ai-response-supports-binary:\n\
  \    description: Stability AI image generation responses should support binary image output\n    message: \"Image operations should return image/jpeg or image/png responses\"\n    severity: warn\n    given: \"$.paths[*].post.responses.200.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stability-ai-seed-parameter:\n    description: Stability AI generation requests should support a seed parameter for reproducibility\n    message: \"Generation request schema should include a seed parameter\"\n    severity: info\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stability-ai/refs/heads/main/rules/stability-ai-rules.yml
tags:
- 3D Generation
- AI
- Generative AI
- Image Generation
- Image Editing
- Machine Learning
- Stable Diffusion
- Text to Image
- Video Generation
- Spectral
- Linting
- API Governance
---
