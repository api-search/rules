---
api_specs:
- filename: red5-server-api-openapi.yml
  format: yaml
  label: Red5 Pro Server API
  slug: server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-server-api-openapi.yml
- filename: red5-stream-manager-2-openapi.yml
  format: yaml
  label: Red5 Pro Stream Manager 2.0 API
  slug: stream-manager-2-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-stream-manager-2-openapi.yml
- filename: red5-brew-mixer-api-openapi.yml
  format: yaml
  label: Red5 Pro Brew Mixer API
  slug: brew-mixer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-brew-mixer-api-openapi.yml
- filename: red5-restreamer-api-openapi.yml
  format: yaml
  label: Red5 Pro Restreamer API
  slug: restreamer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-restreamer-api-openapi.yml
- filename: red5-webrtc-streaming-asyncapi.yml
  format: yaml
  label: Red5 Pro WebRTC SDK
  slug: webrtc-sdk
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/asyncapi/red5-webrtc-streaming-asyncapi.yml
categories:
- red5
description: Spectral linting rules defining API design standards and conventions for Red5.
layout: rules
name: Red5 API Rules
provider_name: Red5
provider_slug: red5
rule_count: 11
rules:
- description: Red5 Pro Server API endpoints authenticate via an accessToken query parameter. All protected endpoints must define this parameter.
  given: $.components.parameters.accessTokenParam
  name: red5-access-token-parameter
  severity: error
- description: All Red5 API operations must include an operationId for SDK generation, tooling integration, and API client code generation.
  given: $.paths[*][get,post,put,delete,patch]
  name: red5-operation-id-required
  severity: error
- description: Operation summaries must use Title Case formatting to match the Red5 Pro API documentation standards.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: red5-summary-title-case
  severity: warn
- description: All Red5 API operations must include descriptions explaining what the endpoint does and the parameters it accepts.
  given: $.paths[*][get,post,put,delete,patch]
  name: red5-operation-description
  severity: warn
- description: All operations must include at least one tag to organize them in API documentation and client libraries.
  given: $.paths[*][get,post,put,delete,patch]
  name: red5-tags-required
  severity: warn
- description: All Red5 API endpoints that require authentication must define a 401 Unauthorized response for invalid or missing access tokens.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: red5-unauthorized-response
  severity: warn
- description: Endpoints that access specific resources (with path parameters like appName and streamName) must define a 404 response.
  given: $.paths[*~@contains('{')][get,post,put,delete].responses
  name: red5-not-found-response
  severity: warn
- description: Red5 Pro Server API is served at port 5080. The server URL must reflect this to ensure clients connect to the correct port.
  given: $.servers[?(@.description === 'Red5 Pro Server')]
  name: red5-server-port
  severity: error
- description: All parameters must define their data type schema for type validation and documentation generation.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: red5-parameter-types
  severity: warn
- description: All 200 responses should reference a defined schema to document the structure of the returned data.
  given: $.paths[*][get].responses[200].content.application/json
  name: red5-response-schema
  severity: warn
- description: Action path segments (e.g., /action/startrecord) must use lowercase to follow Red5 API naming conventions.
  given: $.paths[*~@contains('/action/')]
  name: red5-action-paths
  severity: warn
rules_file: rules/red5-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/rules/red5-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 8
slug: red5-rules
source_filename: red5-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Red5 API uses accessToken query parameter\n  red5-access-token-parameter:\n    description: >-\n      Red5 Pro Server API endpoints authenticate via an accessToken query\n      parameter. All protected endpoints must define this parameter.\n    severity: error\n    given: $.components.parameters.accessTokenParam\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^accessToken$\"\n\n  # Operation IDs required\n  red5-operation-id-required:\n    description: >-\n      All Red5 API operations must include an operationId for SDK generation,\n      tooling integration, and API client code generation.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  # Summary must use Title Case\n  red5-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case formatting to match the\n      Red5 Pro API\
  \ documentation standards.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # Operations need descriptions\n  red5-operation-description:\n    description: >-\n      All Red5 API operations must include descriptions explaining what\n      the endpoint does and the parameters it accepts.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  # Tags must be used consistently\n  red5-tags-required:\n    description: >-\n      All operations must include at least one tag to organize them in\n      API documentation and client libraries.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  # 401 response for all authenticated endpoints\n  red5-unauthorized-response:\n    description: >-\n      All Red5 API\
  \ endpoints that require authentication must define a\n      401 Unauthorized response for invalid or missing access tokens.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      field: '401'\n      function: truthy\n\n  # 404 response for resource-specific endpoints\n  red5-not-found-response:\n    description: >-\n      Endpoints that access specific resources (with path parameters like\n      appName and streamName) must define a 404 response.\n    severity: warn\n    given: $.paths[*~@contains('{')][get,post,put,delete].responses\n    then:\n      field: '404'\n      function: truthy\n\n  # Server URL must include port 5080\n  red5-server-port:\n    description: >-\n      Red5 Pro Server API is served at port 5080. The server URL must\n      reflect this to ensure clients connect to the correct port.\n    severity: error\n    given: $.servers[?(@.description === 'Red5 Pro Server')]\n    then:\n      field: url\n      function: pattern\n \
  \     functionOptions:\n        match: \"5080\"\n\n  # Query parameters should have types defined\n  red5-parameter-types:\n    description: >-\n      All parameters must define their data type schema for type validation\n      and documentation generation.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # Response schemas for 200 responses\n  red5-response-schema:\n    description: >-\n      All 200 responses should reference a defined schema to document\n      the structure of the returned data.\n    severity: warn\n    given: $.paths[*][get].responses[200].content.application/json\n    then:\n      field: schema\n      function: truthy\n\n  # Actions path segments should use lowercase\n  red5-action-paths:\n    description: >-\n      Action path segments (e.g., /action/startrecord) must use lowercase\n      to follow Red5 API naming conventions.\n    severity: warn\n    given: $.paths[*~@contains('/action/')]\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z0-9{}/_-]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/rules/red5-rules.yml
tags:
- Live Streaming
- Media
- Real-Time
- RTMP
- Streaming
- Video
- WebRTC
- Spectral
- Linting
- API Governance
---
