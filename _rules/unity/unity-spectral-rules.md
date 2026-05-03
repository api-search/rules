---
api_specs:
- filename: unity-player-authentication-openapi.yml
  format: yaml
  label: Unity Player Authentication API
  slug: player-authentication
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-player-authentication-openapi.yml
- filename: unity-cloud-code-openapi.yml
  format: yaml
  label: Unity Cloud Code API
  slug: cloud-code
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-cloud-code-openapi.yml
- filename: unity-cloud-save-openapi.yml
  format: yaml
  label: Unity Cloud Save API
  slug: cloud-save
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-cloud-save-openapi.yml
- filename: unity-economy-openapi.yml
  format: yaml
  label: Unity Economy API
  slug: economy
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-economy-openapi.yml
- filename: unity-leaderboards-openapi.yml
  format: yaml
  label: Unity Leaderboards API
  slug: leaderboards
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-leaderboards-openapi.yml
- filename: unity-remote-config-openapi.yml
  format: yaml
  label: Unity Remote Config API
  slug: remote-config
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-remote-config-openapi.yml
- filename: unity-analytics-openapi.yml
  format: yaml
  label: Unity Analytics API
  slug: analytics
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-analytics-openapi.yml
- filename: unity-lobby-openapi.yml
  format: yaml
  label: Unity Lobby API
  slug: lobby
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-lobby-openapi.yml
- filename: unity-matchmaker-openapi.yml
  format: yaml
  label: Unity Matchmaker API
  slug: matchmaker
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-matchmaker-openapi.yml
- filename: unity-relay-openapi.yml
  format: yaml
  label: Unity Relay API
  slug: relay
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-relay-openapi.yml
- filename: unity-multiplay-openapi.yml
  format: yaml
  label: Unity Multiplay Game Server Hosting API
  slug: multiplay-game-server-hosting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-multiplay-openapi.yml
- filename: unity-cloud-content-delivery-openapi.yml
  format: yaml
  label: Unity Cloud Content Delivery API
  slug: cloud-content-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-cloud-content-delivery-openapi.yml
- filename: unity-triggers-openapi.yml
  format: yaml
  label: Unity Triggers API
  slug: triggers
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-triggers-openapi.yml
- filename: unity-scheduler-openapi.yml
  format: yaml
  label: Unity Scheduler API
  slug: scheduler
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-scheduler-openapi.yml
- filename: unity-friends-openapi.yml
  format: yaml
  label: Unity Friends API
  slug: friends
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-friends-openapi.yml
- filename: unity-moderation-openapi.yml
  format: yaml
  label: Unity Moderation API
  slug: moderation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-moderation-openapi.yml
- filename: unity-push-notifications-openapi.yml
  format: yaml
  label: Unity Push Notifications API
  slug: push-notifications
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-push-notifications-openapi.yml
- filename: unity-build-automation-openapi.yml
  format: yaml
  label: Unity Build Automation API
  slug: build-automation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-build-automation-openapi.yml
- filename: unity-version-control-openapi.yml
  format: yaml
  label: Unity Version Control API
  slug: version-control
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-version-control-openapi.yml
- filename: unity-access-openapi.yml
  format: yaml
  label: Unity Access API
  slug: access
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-access-openapi.yml
- filename: unity-scim-openapi.yml
  format: yaml
  label: Unity SCIM API
  slug: scim
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-scim-openapi.yml
- filename: unity-distributed-authority-openapi.yml
  format: yaml
  label: Unity Distributed Authority API
  slug: distributed-authority
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-distributed-authority-openapi.yml
- filename: unity-safe-text-openapi.yml
  format: yaml
  label: Unity Safe Text API
  slug: safe-text
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-safe-text-openapi.yml
- filename: unity-asset-manager-openapi.yml
  format: yaml
  label: Unity Asset Manager API
  slug: asset-manager
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-asset-manager-openapi.yml
- filename: unity-monetize-openapi.yml
  format: yaml
  label: Unity Monetize API
  slug: monetize
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/openapi/unity-monetize-openapi.yml
categories:
- unity
description: Spectral linting rules defining API design standards and conventions for Unity.
layout: rules
name: Unity API Rules
provider_name: Unity
provider_slug: unity
rule_count: 16
rules:
- description: All Unity API paths must start with a version prefix (e.g., /v1/, /v2/, /v3/)
  given: $.paths[*]~
  name: unity-paths-start-with-version
  severity: error
- description: Unity API path segments must use kebab-case (lowercase with hyphens)
  given: $.paths[*]~
  name: unity-paths-use-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths[*]~
  name: unity-no-trailing-slash
  severity: error
- description: Paths that contain projectId or environmentId must include both
  given: $.paths[*]~
  name: unity-project-environment-paths
  severity: hint
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: unity-operation-id-format
  severity: error
- description: All Unity API operations must have an operationId
  given: $.paths[*][*]
  name: unity-operation-id-required
  severity: error
- description: All operations must document at least one 2xx success response
  given: $.paths[*][*].responses
  name: unity-success-response-required
  severity: error
- description: Protected Unity endpoints should document 401 Unauthorized responses
  given: $.paths[*][post,put,patch,delete].responses
  name: unity-401-response-on-secured-endpoints
  severity: warn
- description: Unity APIs use Bearer JWT tokens for authentication
  given: $.components.securitySchemes[*]
  name: unity-bearer-auth-scheme
  severity: info
- description: API info must include a description
  given: $.info
  name: unity-info-description
  severity: error
- description: API must have a version in semver-like format
  given: $.info.version
  name: unity-info-version
  severity: warn
- description: Unity APIs should link to their documentation pages
  given: $
  name: unity-external-docs
  severity: warn
- description: All 2xx responses should have defined schemas
  given: $.paths[*][*].responses[?(@property.match(/^2/))].content.application/json
  name: unity-response-schema-defined
  severity: warn
- description: All path and query parameters should have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path' || @.in == 'query')]
  name: unity-parameters-have-description
  severity: warn
- description: All Unity operations must be tagged for grouping in documentation
  given: $.paths[*][*]
  name: unity-operations-have-tags
  severity: error
- description: Unity API tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: unity-tags-title-case
  severity: warn
rules_file: rules/unity-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/rules/unity-spectral-rules.yml
severity_counts:
  error: 7
  hint: 1
  info: 1
  warn: 7
slug: unity-spectral-rules
source_filename: unity-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # Unity API path structure rules\n  unity-paths-start-with-version:\n    description: All Unity API paths must start with a version prefix (e.g., /v1/, /v2/, /v3/)\n    message: \"Path '{{property}}' must start with a version prefix like /v1/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  unity-paths-use-kebab-case:\n    description: Unity API path segments must use kebab-case (lowercase with hyphens)\n    message: \"Path '{{property}}' must use kebab-case for all segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z_]\"\n\n  unity-no-trailing-slash:\n    description: Paths must not have a trailing slash\n    message: \"Path '{{property}}' must not have a trailing slash\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        notMatch: \"/$\"\n\n  # Unity project and environment path parameters\n  unity-project-environment-paths:\n    description: Paths that contain projectId or environmentId must include both\n    message: \"Paths with projectId should also include environmentId for proper scoping\"\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\{projectId\\\\}(?!.*(?:\\\\{environmentId\\\\}|builds|buildtargets))\"\n\n  # Unity operation ID conventions\n  unity-operation-id-format:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  unity-operation-id-required:\n    description: All Unity API operations must have an operationId\n    message: \"Operation must have an\
  \ operationId for SDK generation compatibility\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Unity response conventions\n  unity-success-response-required:\n    description: All operations must document at least one 2xx success response\n    message: \"Operation must have at least one 2xx response code\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  unity-401-response-on-secured-endpoints:\n    description: Protected Unity endpoints should document 401 Unauthorized responses\n    message: \"Secured endpoint should document 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: defined\n\n  # Unity authentication conventions\n  unity-bearer-auth-scheme:\n    description: Unity APIs use Bearer\
  \ JWT tokens for authentication\n    message: \"Security scheme should use HTTP Bearer authentication\"\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              enum:\n                - http\n                - apiKey\n            scheme:\n              enum:\n                - bearer\n                - basic\n\n  # Unity info requirements\n  unity-info-description:\n    description: API info must include a description\n    message: \"API info must have a description explaining the service purpose\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  unity-info-version:\n    description: API must have a version in semver-like format\n    message: \"API version '{{value}}' should follow vX.Y.Z or vX format\"\n    severity: warn\n    given: \"$.info.version\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^v[0-9]\"\n\n  unity-external-docs:\n    description: Unity APIs should link to their documentation pages\n    message: \"API should include externalDocs linking to Unity documentation\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n\n  # Unity schema conventions\n  unity-response-schema-defined:\n    description: All 2xx responses should have defined schemas\n    message: \"Response must include a content schema definition\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property.match(/^2/))].content.application/json\"\n    then:\n      field: schema\n      function: defined\n\n  unity-parameters-have-description:\n    description: All path and query parameters should have descriptions\n    message: \"Parameter '{{property}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path' || @.in == 'query')]\"\n\
  \    then:\n      field: description\n      function: truthy\n\n  # Unity tag conventions\n  unity-operations-have-tags:\n    description: All Unity operations must be tagged for grouping in documentation\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  unity-tags-title-case:\n    description: Unity API tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unity/refs/heads/main/rules/unity-spectral-rules.yml
tags:
- Game Development
- Real-Time 3D
- Multiplayer
- Game Services
- Cloud Gaming
- Spectral
- Linting
- API Governance
---
