---
api_specs:
- filename: strava-openapi.yml
  format: yaml
  label: Strava API
  slug: strava
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strava/refs/heads/main/openapi/strava-openapi.yml
categories:
- strava
description: Spectral linting rules defining API design standards and conventions for Strava.
layout: rules
name: Strava API Rules
provider_name: Strava
provider_slug: strava
rule_count: 10
rules:
- description: Strava API uses camelCase operationIds (e.g., getLoggedInAthlete, getActivityById, getLeaderboardBySegmentId).
  given: $.paths[*][*].operationId
  name: strava-operation-ids-camel-case
  severity: warn
- description: All OpenAPI tags must use Title Case (e.g., 'Athletes', 'Activities', 'Segment Efforts').
  given: $.tags[*].name
  name: strava-tags-title-case
  severity: warn
- description: All Strava API operations must use OAuth 2.0 Bearer token security. The security scheme must be stravaBearerAuth.
  given: $.components.securitySchemes
  name: strava-oauth2-security
  severity: warn
- description: Strava list endpoints use per_page (not pageSize) for pagination with a maximum of 200 items per page. page parameter starts at 1.
  given: $.paths[*][get].parameters[*].name
  name: strava-pagination-per-page
  severity: info
- description: Strava resource IDs (athletes, activities, segments, clubs, routes) use integer identifiers. Only gear IDs are strings (prefixed with 'b' for bikes or 'g' for shoes).
  given: $.paths['/athletes/{id}/stats', '/activities/{id}', '/segments/{id}', '/clubs/{id}', '/routes/{id}', '/segment_efforts/{id}'][*].parameters[?(@.name == 'id')].schema
  name: strava-resource-ids-integer
  severity: info
- description: Strava list endpoints return arrays directly at the top level (not wrapped in a data object). Individual resources return objects directly.
  given: $.paths[?(@property.startsWith('/athlete/') && @property != '/athlete' && @property != '/athlete/zones')][get].responses['200'].content['application/json'].schema
  name: strava-response-arrays-for-lists
  severity: info
- description: Activity type fields should include documentation about supported sport types (Run, Ride, Swim, Walk, Hike, VirtualRide, etc.).
  given: $.components.schemas.DetailedActivity.properties.type
  name: strava-activity-type-documented
  severity: info
- description: The Strava API has rate limits (100 requests/15 min, 1000/day). API documentation should reference rate limit policies.
  given: $.info
  name: strava-rate-limit-documented
  severity: info
- description: All operations must have a summary. Strava uses action-noun format (e.g., 'Get Activity', 'List Athlete Activities').
  given: $.paths[*][get,post,put,delete]
  name: strava-operation-summaries-present
  severity: error
- description: The Strava streams endpoints require the 'keys' parameter to specify which stream types to return.
  given: $.paths['/activities/{id}/streams'][get].parameters[?(@.name == 'keys')]
  name: strava-streams-keys-required
  severity: warn
rules_file: rules/strava-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/strava/refs/heads/main/rules/strava-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 5
  warn: 4
slug: strava-rules
source_filename: strava-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  strava-operation-ids-camel-case:\n    description: >-\n      Strava API uses camelCase operationIds (e.g., getLoggedInAthlete,\n      getActivityById, getLeaderboardBySegmentId).\n    message: \"OperationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  strava-tags-title-case:\n    description: >-\n      All OpenAPI tags must use Title Case (e.g., 'Athletes', 'Activities',\n      'Segment Efforts').\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  strava-oauth2-security:\n    description: >-\n      All Strava API operations must use OAuth 2.0 Bearer token security.\n      The security scheme must be stravaBearerAuth.\n\
  \    message: \"Strava API requires OAuth 2.0 via stravaBearerAuth\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: \"stravaBearerAuth\"\n\n  strava-pagination-per-page:\n    description: >-\n      Strava list endpoints use per_page (not pageSize) for pagination with\n      a maximum of 200 items per page. page parameter starts at 1.\n    message: \"Strava list endpoints should use per_page pagination parameter\"\n    severity: info\n    given: \"$.paths[*][get].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^pageSize$|^limit$\"\n\n  strava-resource-ids-integer:\n    description: >-\n      Strava resource IDs (athletes, activities, segments, clubs, routes)\n      use integer identifiers. Only gear IDs are strings (prefixed with\n      'b' for bikes or 'g' for shoes).\n    message: \"Path parameter 'id' for non-gear resources should be integer type\"\n    severity: info\n\
  \    given: \"$.paths['/athletes/{id}/stats', '/activities/{id}', '/segments/{id}', '/clubs/{id}', '/routes/{id}', '/segment_efforts/{id}'][*].parameters[?(@.name == 'id')].schema\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  strava-response-arrays-for-lists:\n    description: >-\n      Strava list endpoints return arrays directly at the top level (not\n      wrapped in a data object). Individual resources return objects directly.\n    message: \"List endpoints should return an array response\"\n    severity: info\n    given: \"$.paths[?(@property.startsWith('/athlete/') && @property != '/athlete' && @property != '/athlete/zones')][get].responses['200'].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              const: \"array\"\n\n  strava-activity-type-documented:\n    description: >-\n   \
  \   Activity type fields should include documentation about supported sport\n      types (Run, Ride, Swim, Walk, Hike, VirtualRide, etc.).\n    message: \"Activity type field should have a description\"\n    severity: info\n    given: \"$.components.schemas.DetailedActivity.properties.type\"\n    then:\n      function: truthy\n      field: \"description\"\n\n  strava-rate-limit-documented:\n    description: >-\n      The Strava API has rate limits (100 requests/15 min, 1000/day).\n      API documentation should reference rate limit policies.\n    message: \"API info should reference rate limit documentation\"\n    severity: info\n    given: \"$.info\"\n    then:\n      function: truthy\n      field: \"description\"\n\n  strava-operation-summaries-present:\n    description: >-\n      All operations must have a summary. Strava uses action-noun\n      format (e.g., 'Get Activity', 'List Athlete Activities').\n    message: \"Operation must have a summary\"\n    severity: error\n    given:\
  \ \"$.paths[*][get,post,put,delete]\"\n    then:\n      function: truthy\n      field: \"summary\"\n\n  strava-streams-keys-required:\n    description: >-\n      The Strava streams endpoints require the 'keys' parameter to specify\n      which stream types to return.\n    message: \"Streams endpoint must have 'keys' as a required parameter\"\n    severity: warn\n    given: \"$.paths['/activities/{id}/streams'][get].parameters[?(@.name == 'keys')]\"\n    then:\n      function: truthy\n      field: \"required\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/strava/refs/heads/main/rules/strava-rules.yml
tags:
- Cycling
- Fitness
- Fitness Tracking
- Running
- Sports
- Spectral
- Linting
- API Governance
---
