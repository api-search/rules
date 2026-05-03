---
api_specs:
- filename: streamyard-openapi.yml
  format: yaml
  label: StreamYard API
  slug: streamyard-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/streamyard/refs/heads/main/openapi/streamyard-openapi.yml
categories:
- streamyard
description: Spectral linting rules defining API design standards and conventions for StreamYard.
layout: rules
name: StreamYard API Rules
provider_name: StreamYard
provider_slug: streamyard
rule_count: 9
rules:
- description: StreamYard API operationIds use camelCase (e.g., listBroadcasts, createBroadcast, getBroadcast).
  given: $.paths[*][*].operationId
  name: streamyard-operation-ids-camel-case
  severity: warn
- description: All OpenAPI tags must use Title Case (e.g., 'Broadcasts', 'Destinations', 'Recordings').
  given: $.tags[*].name
  name: streamyard-tags-title-case
  severity: warn
- description: StreamYard API requires OAuth 2.0 authentication. The security scheme must be streamyardBearerAuth using the authorization code flow.
  given: $.components.securitySchemes
  name: streamyard-oauth2-security
  severity: warn
- description: Broadcast-specific endpoints use broadcastId as the path parameter name for consistency.
  given: $.components.parameters.BroadcastId
  name: streamyard-broadcast-id-path-param
  severity: warn
- description: DELETE operations in the StreamYard API return 204 No Content on successful deletion.
  given: $.paths[*][delete].responses
  name: streamyard-delete-returns-204
  severity: info
- description: 'Broadcast status must be one of the defined enum values: created, live, completed, cancelled.'
  given: $.components.schemas.Broadcast.properties.status
  name: streamyard-broadcast-status-enum
  severity: warn
- description: 'Destination platform must be one of the supported streaming platforms: youtube, facebook, linkedin, twitter, twitch, rtmp.'
  given: $.components.schemas.Destination.properties.platform
  name: streamyard-platform-enum
  severity: warn
- description: 'StreamYard uses camelCase pagination parameters: page and perPage (not per_page or pageSize).'
  given: $.paths[*][get].parameters[*].name
  name: streamyard-pagination-camel-case
  severity: info
- description: All operations must have a summary in Title Case format.
  given: $.paths[*][get,post,put,patch,delete]
  name: streamyard-operation-summaries-present
  severity: error
rules_file: rules/streamyard-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/streamyard/refs/heads/main/rules/streamyard-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 6
slug: streamyard-rules
source_filename: streamyard-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  streamyard-operation-ids-camel-case:\n    description: >-\n      StreamYard API operationIds use camelCase (e.g., listBroadcasts,\n      createBroadcast, getBroadcast).\n    message: \"OperationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  streamyard-tags-title-case:\n    description: >-\n      All OpenAPI tags must use Title Case (e.g., 'Broadcasts', 'Destinations',\n      'Recordings').\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  streamyard-oauth2-security:\n    description: >-\n      StreamYard API requires OAuth 2.0 authentication. The security scheme\n      must be streamyardBearerAuth using\
  \ the authorization code flow.\n    message: \"API must use streamyardBearerAuth OAuth 2.0 security scheme\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: \"streamyardBearerAuth\"\n\n  streamyard-broadcast-id-path-param:\n    description: >-\n      Broadcast-specific endpoints use broadcastId as the path parameter\n      name for consistency.\n    message: \"Broadcast path parameter must be named 'broadcastId'\"\n    severity: warn\n    given: \"$.components.parameters.BroadcastId\"\n    then:\n      field: \"name\"\n      function: enumeration\n      functionOptions:\n        values:\n          - broadcastId\n\n  streamyard-delete-returns-204:\n    description: >-\n      DELETE operations in the StreamYard API return 204 No Content on\n      successful deletion.\n    message: \"DELETE operation should return 204 on success\"\n    severity: info\n    given: \"$.paths[*][delete].responses\"\n    then:\n      function: truthy\n\
  \      field: \"204\"\n\n  streamyard-broadcast-status-enum:\n    description: >-\n      Broadcast status must be one of the defined enum values: created, live,\n      completed, cancelled.\n    message: \"Broadcast status must be a valid enum value\"\n    severity: warn\n    given: \"$.components.schemas.Broadcast.properties.status\"\n    then:\n      function: truthy\n      field: \"enum\"\n\n  streamyard-platform-enum:\n    description: >-\n      Destination platform must be one of the supported streaming platforms:\n      youtube, facebook, linkedin, twitter, twitch, rtmp.\n    message: \"Platform must be a defined enum value\"\n    severity: warn\n    given: \"$.components.schemas.Destination.properties.platform\"\n    then:\n      function: truthy\n      field: \"enum\"\n\n  streamyard-pagination-camel-case:\n    description: >-\n      StreamYard uses camelCase pagination parameters: page and perPage\n      (not per_page or pageSize).\n    message: \"Pagination parameter should use\
  \ camelCase (perPage not per_page)\"\n    severity: info\n    given: \"$.paths[*][get].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^per_page$|^pageSize$\"\n\n  streamyard-operation-summaries-present:\n    description: >-\n      All operations must have a summary in Title Case format.\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: truthy\n      field: \"summary\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/streamyard/refs/heads/main/rules/streamyard-rules.yml
tags:
- Broadcasting
- Live Streaming
- Multi-Streaming
- Recordings
- Video
- Spectral
- Linting
- API Governance
---
