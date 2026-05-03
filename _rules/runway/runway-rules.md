---
api_specs:
- filename: runway-video-generation-openapi.yml
  format: yaml
  label: Runway Video Generation API
  slug: video-generation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-video-generation-openapi.yml
- filename: runway-image-generation-openapi.yml
  format: yaml
  label: Runway Image Generation API
  slug: image-generation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-image-generation-openapi.yml
- filename: runway-characters-openapi.yml
  format: yaml
  label: Runway Characters API
  slug: characters
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-characters-openapi.yml
categories:
- runway
description: Spectral linting rules defining API design standards and conventions for Runway.
layout: rules
name: Runway API Rules
provider_name: Runway
provider_slug: runway
rule_count: 17
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: runway-operation-id-required
  severity: error
- description: Runway operationIds use camelCase convention (e.g., createTextToVideo, getTask, createAvatar). This ensures consistent client SDK method naming across Python and Node.js SDKs.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: runway-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: runway-tags-required
  severity: error
- description: Tags must use Title Case (e.g., "Tasks", "Text to Video", "Image to Video", "Avatars", "Documents", "Realtime Sessions").
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: runway-tags-title-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: runway-summary-required
  severity: error
- description: Operation summaries must use Title Case to match Runway's documentation (e.g., "Create Text-to-Video Generation Task", "Retrieve Task Status and Output").
  given: $.paths[*][get,post,put,patch,delete].summary
  name: runway-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: runway-description-required
  severity: warn
- description: All Runway API operations require the X-Runway-Version header set to "2024-11-06". This should be documented as a required parameter in every operation.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'X-Runway-Version')]
  name: runway-version-header-required
  severity: warn
- description: Runway API uses Bearer token authentication. All operations must be secured by the bearerAuth security scheme.
  given: $.paths[*][get,post,put,patch,delete]
  name: runway-bearer-auth-required
  severity: error
- description: 'Runway generation endpoints follow an async task pattern: POST creates a task and returns a TaskCreatedResponse with an id field. GET /tasks/{id} polls for completion. All generation POST endpoints should return a task creation response.'
  given: $.paths[/image_to_video,/text_to_video,/video_to_video,/character_performance,/lip_sync,/video_upscale,/frame_interpolation,/sound_effect,/text_to_image].post.responses.200.content.application/json.schema
  name: runway-post-creates-task-pattern
  severity: info
- description: 'Task IDs in Runway API are UUIDs. Path parameters named "id" for task operations should specify format: uuid.'
  given: $.paths[~/tasks/~][*].parameters[?(@.name == 'id')].schema
  name: runway-task-id-uuid-format
  severity: warn
- description: Runway API enforces rate limits. Generation POST endpoints should document the 429 Too Many Requests response.
  given: $.paths[/image_to_video,/text_to_video,/video_to_video,/text_to_image,/character_performance,/lip_sync,/video_upscale,/frame_interpolation,/sound_effect].post.responses
  name: runway-429-rate-limit-documented
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: runway-delete-returns-204
  severity: warn
- description: All operations must document the 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: runway-response-must-have-401
  severity: error
- description: All schema properties should have a type defined
  given: $.components.schemas[*].properties[*]
  name: runway-schema-properties-typed
  severity: warn
- description: Runway API production server URL is https://api.dev.runwayml.com/v1. The server must be documented correctly.
  given: $.servers[*].url
  name: runway-servers-use-production-url
  severity: warn
- description: Runway API uses date-based versioning in YYYY-MM-DD format (e.g., "2024-11-06"). The info.version field should reflect the API date version.
  given: $.info.version
  name: runway-info-version-format
  severity: warn
rules_file: rules/runway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/rules/runway-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 11
slug: runway-rules
source_filename: runway-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  runway-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  runway-operation-id-camel-case:\n    description: >-\n      Runway operationIds use camelCase convention (e.g., createTextToVideo,\n      getTask, createAvatar). This ensures consistent client SDK method naming\n      across Python and Node.js SDKs.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  runway-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  runway-tags-title-case:\n    description: >-\n      Tags must use Title\
  \ Case (e.g., \"Tasks\", \"Text to Video\", \"Image to Video\",\n      \"Avatars\", \"Documents\", \"Realtime Sessions\").\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  runway-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  runway-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case to match Runway's documentation\n      (e.g., \"Create Text-to-Video Generation Task\", \"Retrieve Task Status and Output\").\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 \\\\-]+$\"\n\n  runway-description-required:\n    description: All operations\
  \ must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  runway-version-header-required:\n    description: >-\n      All Runway API operations require the X-Runway-Version header set to \"2024-11-06\".\n      This should be documented as a required parameter in every operation.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'X-Runway-Version')]\"\n    then:\n      field: required\n      function: truthy\n\n  runway-bearer-auth-required:\n    description: >-\n      Runway API uses Bearer token authentication. All operations must be secured\n      by the bearerAuth security scheme.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - description: Security inherited\
  \ from global level\n\n  runway-post-creates-task-pattern:\n    description: >-\n      Runway generation endpoints follow an async task pattern: POST creates a task\n      and returns a TaskCreatedResponse with an id field. GET /tasks/{id} polls for\n      completion. All generation POST endpoints should return a task creation response.\n    severity: info\n    given: \"$.paths[/image_to_video,/text_to_video,/video_to_video,/character_performance,/lip_sync,/video_upscale,/frame_interpolation,/sound_effect,/text_to_image].post.responses.200.content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  runway-task-id-uuid-format:\n    description: >-\n      Task IDs in Runway API are UUIDs. Path parameters named \"id\" for task operations\n      should specify format: uuid.\n    severity: warn\n    given: \"$.paths[~/tasks/~][*].parameters[?(@.name == 'id')].schema\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n\
  \        values:\n          - uuid\n\n  runway-429-rate-limit-documented:\n    description: >-\n      Runway API enforces rate limits. Generation POST endpoints should document\n      the 429 Too Many Requests response.\n    severity: warn\n    given: \"$.paths[/image_to_video,/text_to_video,/video_to_video,/text_to_image,/character_performance,/lip_sync,/video_upscale,/frame_interpolation,/sound_effect].post.responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  runway-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  runway-response-must-have-401:\n    description: All operations must document the 401 Unauthorized response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  runway-schema-properties-typed:\n    description:\
  \ All schema properties should have a type defined\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  runway-servers-use-production-url:\n    description: >-\n      Runway API production server URL is https://api.dev.runwayml.com/v1.\n      The server must be documented correctly.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"api\\\\.dev\\\\.runwayml\\\\.com\"\n\n  runway-info-version-format:\n    description: >-\n      Runway API uses date-based versioning in YYYY-MM-DD format (e.g., \"2024-11-06\").\n      The info.version field should reflect the API date version.\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^20[0-9]{2}-[0-1][0-9]-[0-3][0-9]$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/rules/runway-rules.yml
tags:
- Video Generation
- Image Generation
- Artificial Intelligence
- Machine Learning
- Generative AI
- Avatars
- Characters
- WebRTC
- Creative Tools
- Spectral
- Linting
- API Governance
---
