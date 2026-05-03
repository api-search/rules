---
api_specs:
- filename: spotify-openapi-original.yml
  format: yaml
  label: Spotify Web API
  slug: spotify-web-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spotify/refs/heads/main/openapi/spotify-openapi-original.yml
categories:
- spotify
description: Spectral linting rules defining API design standards and conventions for Spotify.
layout: rules
name: Spotify API Rules
provider_name: Spotify
provider_slug: spotify
rule_count: 14
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-operation-ids-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-operation-summary-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-tags-required
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: spotify-response-200-get
  severity: error
- description: All operations must document 401 Unauthorized (OAuth required)
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-response-401-required
  severity: error
- description: All operations should document 403 Forbidden (scope missing)
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-response-403-required
  severity: warn
- description: All operations must document 429 Too Many Requests
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-response-429-required
  severity: error
- description: API must use OAuth 2.0 security scheme
  given: $.components.securitySchemes.oauth_2_0
  name: spotify-oauth2-security
  severity: error
- description: Path parameters for IDs should use underscore_case naming
  given: $.paths[*]~
  name: spotify-path-ids-use-kebab
  severity: info
- description: List endpoints should support a 'limit' query parameter
  given: $.paths[?(@property.match(/\/tracks$|\/albums$|\/artists$|\/playlists$|\/items$|\/episodes$/))]..parameters[?(@.name == 'limit')]
  name: spotify-pagination-limit-param
  severity: warn
- description: Spotify URI fields should follow spotify:{type}:{id} pattern
  given: $.components.schemas[*].properties.uri
  name: spotify-spotify-uri-format
  severity: info
- description: Market parameters should be named 'market' and use ISO 3166-1 codes
  given: $.paths[*][get,post].parameters[?(@.name == 'market')]
  name: spotify-market-param-naming
  severity: info
- description: Success responses must include a schema
  given: $.paths[*].get.responses['200'].content.application/json
  name: spotify-response-schema-required
  severity: warn
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: spotify-description-required
  severity: warn
rules_file: rules/spotify-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spotify/refs/heads/main/rules/spotify-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 3
  warn: 4
slug: spotify-rules
source_filename: spotify-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spotify-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spotify-operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  spotify-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spotify-response-200-get:\n    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  spotify-response-401-required:\n    description: All operations must document\
  \ 401 Unauthorized (OAuth required)\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  spotify-response-403-required:\n    description: All operations should document 403 Forbidden (scope missing)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.403\n      function: truthy\n\n  spotify-response-429-required:\n    description: All operations must document 429 Too Many Requests\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.429\n      function: truthy\n\n  spotify-oauth2-security:\n    description: API must use OAuth 2.0 security scheme\n    severity: error\n    given: \"$.components.securitySchemes.oauth_2_0\"\n    then:\n      function: truthy\n\n  spotify-path-ids-use-kebab:\n    description: Path parameters for IDs should use underscore_case naming\n    severity: info\n  \
  \  given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z_{}]+)+$\"\n\n  spotify-pagination-limit-param:\n    description: List endpoints should support a 'limit' query parameter\n    severity: warn\n    given: \"$.paths[?(@property.match(/\\\\/tracks$|\\\\/albums$|\\\\/artists$|\\\\/playlists$|\\\\/items$|\\\\/episodes$/))]..parameters[?(@.name == 'limit')]\"\n    then:\n      function: truthy\n\n  spotify-spotify-uri-format:\n    description: Spotify URI fields should follow spotify:{type}:{id} pattern\n    severity: info\n    given: \"$.components.schemas[*].properties.uri\"\n    then:\n      function: truthy\n\n  spotify-market-param-naming:\n    description: Market parameters should be named 'market' and use ISO 3166-1 codes\n    severity: info\n    given: \"$.paths[*][get,post].parameters[?(@.name == 'market')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\
  \n  spotify-response-schema-required:\n    description: Success responses must include a schema\n    severity: warn\n    given: \"$.paths[*].get.responses['200'].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  spotify-description-required:\n    description: Operations should have descriptions\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spotify/refs/heads/main/rules/spotify-rules.yml
tags:
- Music
- Audio
- Streaming
- Podcasts
- Playlists
- Spectral
- Linting
- API Governance
---
