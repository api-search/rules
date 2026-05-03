---
api_specs:
- filename: salad-transcription-api-openapi.yml
  format: yaml
  label: Salad Transcription API
  slug: salad-transcription-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salad-transcription-api/refs/heads/main/openapi/salad-transcription-api-openapi.yml
categories:
- salad
description: Spectral linting rules defining API design standards and conventions for Salad Transcription API.
layout: rules
name: Salad Transcription API API Rules
provider_name: Salad Transcription API
provider_slug: salad-transcription-api
rule_count: 6
rules:
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: salad-operation-summary-required
  severity: error
- description: Salad API uses Salad-Api-Key header for authentication.
  given: $.paths[*][*].parameters[*]
  name: salad-api-key-header-required
  severity: warn
- description: All operations must define a 200 success response.
  given: $.paths[*][*].responses
  name: salad-response-200-required
  severity: error
- description: Request bodies should use application/json.
  given: $.paths[*][*].requestBody.content
  name: salad-content-type-json
  severity: warn
- description: API info should include contact details.
  given: $.info
  name: salad-info-contact
  severity: hint
- description: API must define at least one server.
  given: $
  name: salad-servers-defined
  severity: error
rules_file: rules/salad-transcription-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salad-transcription-api/refs/heads/main/rules/salad-transcription-api-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 2
slug: salad-transcription-api-rules
source_filename: salad-transcription-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  salad-operation-summary-required:\n    description: All operations must have a summary.\n    message: \"Operation must have a non-empty summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  salad-api-key-header-required:\n    description: Salad API uses Salad-Api-Key header for authentication.\n    message: \"Operation should document Salad-Api-Key header parameter.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                const: Salad-Api-Key\n          then:\n            properties:\n              in:\n                const: header\n\n  salad-response-200-required:\n    description: All operations must define a 200 success response.\n    message: \"Operation must define a 200 success response.\"\n    severity:\
  \ error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n\n  salad-content-type-json:\n    description: Request bodies should use application/json.\n    message: \"Request body should use application/json content type.\"\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"application/json\"]\n\n  salad-info-contact:\n    description: API info should include contact details.\n    message: \"API info should include contact information.\"\n    severity: hint\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salad-servers-defined:\n    description: API must define at least one server.\n    message: \"API must define at least one server URL.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salad-transcription-api/refs/heads/main/rules/salad-transcription-api-rules.yml
tags:
- Audio Transcription
- Captions
- Diarization
- GPU
- Speech Recognition
- Transcription
- Video Processing
- Spectral
- Linting
- API Governance
---
