---
api_specs:
- filename: truefoundry-ai-gateway-openapi.yml
  format: yaml
  label: TrueFoundry AI Gateway API
  slug: truefoundry-ai-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truefoundry/refs/heads/main/openapi/truefoundry-ai-gateway-openapi.yml
categories:
- truefoundry
description: Spectral linting rules defining API design standards and conventions for TrueFoundry.
layout: rules
name: TrueFoundry API Rules
provider_name: TrueFoundry
provider_slug: truefoundry
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: truefoundry-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: truefoundry-operation-tags-required
  severity: error
- description: API must use Bearer authentication
  given: $.components.securitySchemes.*
  name: truefoundry-bearer-auth-required
  severity: error
- description: LLM operations should require a model parameter
  given: $.paths[/chat/completions,/embeddings,/rerank][post].requestBody.content.application/json.schema.required
  name: truefoundry-model-param-required
  severity: warn
- description: POST endpoints should return 200 or 201 for success
  given: $.paths[*][post]
  name: truefoundry-openai-compatible-success
  severity: error
- description: Error responses should include an error object with message field
  given: $.paths[*][*].responses[4*,5*].content.application/json.schema.properties
  name: truefoundry-error-response-shape
  severity: warn
- description: Completion responses should include usage statistics
  given: $.components.schemas.ChatCompletionResponse.properties
  name: truefoundry-usage-in-response
  severity: hint
- description: Chat completions should document streaming support
  given: $.paths[/chat/completions][post].requestBody.content.application/json.schema.properties
  name: truefoundry-streaming-documented
  severity: hint
- description: The API follows OpenAI-compatible conventions for model, messages, and response format
  given: $.paths[/chat/completions][post].requestBody.content.application/json.schema.required
  name: truefoundry-openai-compatibility
  severity: warn
rules_file: rules/truefoundry-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/truefoundry/refs/heads/main/rules/truefoundry-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 4
slug: truefoundry-rules
source_filename: truefoundry-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  truefoundry-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]* ?)+$\"\n\n  truefoundry-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  truefoundry-bearer-auth-required:\n    description: API must use Bearer authentication\n    severity: error\n    given: \"$.components.securitySchemes.*\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n\n  truefoundry-model-param-required:\n    description: LLM operations should require a model parameter\n    severity: warn\n    given: \"$.paths[/chat/completions,/embeddings,/rerank][post].requestBody.content.application/json.schema.required\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: string\n            enum:\n              - model\n\n  truefoundry-openai-compatible-success:\n    description: POST endpoints should return 200 or 201 for success\n    severity: error\n    given: \"$.paths[*][post]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  truefoundry-error-response-shape:\n    description: Error responses should include an error object with message field\n    severity: warn\n    given: \"$.paths[*][*].responses[4*,5*].content.application/json.schema.properties\"\n    then:\n      field: error\n      function: truthy\n\n  truefoundry-usage-in-response:\n    description: Completion responses should include usage statistics\n    severity: hint\n    given: \"$.components.schemas.ChatCompletionResponse.properties\"\n   \
  \ then:\n      field: usage\n      function: truthy\n\n  truefoundry-streaming-documented:\n    description: Chat completions should document streaming support\n    severity: hint\n    given: \"$.paths[/chat/completions][post].requestBody.content.application/json.schema.properties\"\n    then:\n      field: stream\n      function: truthy\n\n  truefoundry-openai-compatibility:\n    description: >-\n      The API follows OpenAI-compatible conventions for model, messages,\n      and response format\n    severity: warn\n    given: \"$.paths[/chat/completions][post].requestBody.content.application/json.schema.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: string\n            enum:\n              - messages\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/truefoundry/refs/heads/main/rules/truefoundry-rules.yml
tags:
- AI Platform
- Enterprise AI
- Kubernetes
- LLM Gateway
- MLOps
- Spectral
- Linting
- API Governance
---
