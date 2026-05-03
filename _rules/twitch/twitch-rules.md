---
api_specs:
- filename: reference
  format: yaml
  label: Twitch API
  slug: ''
  spec_type: OpenAPI
  url: https://dev.twitch.tv/docs/api/reference
- filename: twitch-eventsub-asyncapi.yml
  format: yaml
  label: Twitch EventSub
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/asyncapi/twitch-eventsub-asyncapi.yml
- filename: twitch-extensions-openapi.yml
  format: yaml
  label: Twitch Extensions API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-extensions-openapi.yml
- filename: twitch-drops-openapi.yml
  format: yaml
  label: Twitch Drops API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-drops-openapi.yml
- filename: twitch-video-broadcast-openapi.yml
  format: yaml
  label: Twitch Video Broadcast API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-video-broadcast-openapi.yml
- filename: twitch-insights-analytics-openapi.yml
  format: yaml
  label: Twitch Insights and Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-insights-analytics-openapi.yml
- filename: twitch-igdb-openapi.yml
  format: yaml
  label: IGDB API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-igdb-openapi.yml
categories:
- twitch
description: Spectral linting rules defining API design standards and conventions for Twitch.
layout: rules
name: Twitch API Rules
provider_name: Twitch
provider_slug: twitch
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: twitch-summary-title-case
  severity: warn
- description: Operation summaries should be prefixed with the API product name (e.g. "Twitch")
  given: $.paths[*][*].summary
  name: twitch-summary-provider-prefix
  severity: hint
- description: Twitch operations should reference the clientId parameter
  given: $.paths[*][get,post,patch,put,delete].parameters[*]
  name: twitch-requires-client-id-parameter
  severity: hint
- description: All operations should declare security requirements
  given: $.paths[*][get,post,patch,put,delete]
  name: twitch-security-defined
  severity: warn
- description: Twitch does not use HTTP Basic authentication
  given: $.components.securitySchemes[*]
  name: twitch-no-basic-auth
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: twitch-operation-id-camel-case
  severity: warn
- description: Tags must use Title Case
  given: $.tags[*].name
  name: twitch-tags-title-case
  severity: warn
- description: Operations must define a success response
  given: $.paths[*][get,post,patch,put,delete].responses
  name: twitch-success-response-defined
  severity: error
- description: Path segments must use snake_case or kebab-case (Twitch uses snake_case)
  given: $.paths
  name: twitch-paths-kebab-case
  severity: hint
- description: Collection GET endpoints should support pagination via 'first' and 'after' parameters
  given: $.paths[*][get]
  name: twitch-pagination-first-parameter
  severity: hint
rules_file: rules/twitch-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/rules/twitch-rules.yml
severity_counts:
  error: 2
  hint: 4
  info: 0
  warn: 4
slug: twitch-rules
source_filename: twitch-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Twitch API conventions: all summaries must use Title Case and include the \"Twitch\" prefix\n  twitch-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  twitch-summary-provider-prefix:\n    description: Operation summaries should be prefixed with the API product name (e.g. \"Twitch\")\n    message: \"Summary '{{value}}' should start with a provider or product prefix\"\n    given: \"$.paths[*][*].summary\"\n    severity: hint\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(Twitch|IGDB)\"\n\n  # Twitch requires Client-Id header on all authenticated operations\n  twitch-requires-client-id-parameter:\n    description: Twitch operations should reference the clientId\
  \ parameter\n    message: \"Twitch operations should reference the #/components/parameters/clientId parameter\"\n    given: \"$.paths[*][get,post,patch,put,delete].parameters[*]\"\n    severity: hint\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            $ref:\n              type: string\n\n  # OAuth2 security should be defined\n  twitch-security-defined:\n    description: All operations should declare security requirements\n    message: \"Operation '{{path}}' is missing security declaration\"\n    given: \"$.paths[*][get,post,patch,put,delete]\"\n    severity: warn\n    then:\n      field: security\n      function: truthy\n\n  # Twitch uses bearer/app access tokens; no operation should use basic auth\n  twitch-no-basic-auth:\n    description: Twitch does not use HTTP Basic authentication\n    message: \"Basic authentication is not used in the Twitch API\"\n    given: \"$.components.securitySchemes[*]\"\n\
  \    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          not:\n            properties:\n              scheme:\n                const: basic\n\n  # Operation IDs must use camelCase\n  twitch-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Tags must use Title Case\n  twitch-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # Responses must define at least a 200 or 201\n  twitch-success-response-defined:\n    description: Operations must define a success response\n   \
  \ message: \"Operation must define a 200, 201, or 204 response\"\n    given: \"$.paths[*][get,post,patch,put,delete].responses\"\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # All paths must be kebab-case\n  twitch-paths-kebab-case:\n    description: Path segments must use snake_case or kebab-case (Twitch uses snake_case)\n    message: \"Path '{{path}}' should use lowercase letters with underscores\"\n    given: \"$.paths\"\n    severity: hint\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9_/{}]*)+$\"\n\n  # Pagination parameters should follow Twitch conventions\n  twitch-pagination-first-parameter:\n    description: Collection GET endpoints should support pagination via 'first' and 'after' parameters\n    message: \"Collection endpoints should\
  \ support 'first' and 'after' cursor pagination\"\n    given: \"$.paths[*][get]\"\n    severity: hint\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/rules/twitch-rules.yml
tags:
- Entertainment
- Gaming
- Live Video
- Streaming
- Video
- Spectral
- Linting
- API Governance
---
