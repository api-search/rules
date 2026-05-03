---
api_specs:
- filename: reddit-data-api-openapi.yml
  format: yaml
  label: Reddit Data API
  slug: data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reddit/refs/heads/main/openapi/reddit-data-api-openapi.yml
- filename: reddit-ads-api-openapi.yml
  format: yaml
  label: Reddit Ads API
  slug: ads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reddit/refs/heads/main/openapi/reddit-ads-api-openapi.yml
- filename: reddit-embeds-openapi.yml
  format: yaml
  label: Reddit Embeds (oEmbed)
  slug: embeds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reddit/refs/heads/main/openapi/reddit-embeds-openapi.yml
categories:
- reddit
description: Spectral linting rules defining API design standards and conventions for Reddit.
layout: rules
name: Reddit API Rules
provider_name: Reddit
provider_slug: reddit
rule_count: 12
rules:
- description: All Reddit API operations must use OAuth 2.0 authentication. The oauth2 security scheme must be defined with authorizationCode flow pointing to reddit.com authorization endpoints.
  given: $.components.securitySchemes.oauth2.flows.authorizationCode
  name: reddit-oauth2-security
  severity: error
- description: Reddit API requires a descriptive User-Agent header identifying the application. This must be documented in the API info or parameters.
  given: $.info
  name: reddit-user-agent-required
  severity: warn
- description: Reddit API has strict rate limits (60 req/min for authenticated, 1 req/sec for Ads API). Rate limits must be documented in the API description.
  given: $.info.description
  name: reddit-rate-limits-documented
  severity: warn
- description: All Reddit API operations must have operationIds for SDK generation and tooling support.
  given: $.paths[*][get,post,put,delete,patch]
  name: reddit-operation-id-required
  severity: error
- description: Operation summaries must use Title Case formatting following Reddit API documentation conventions.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: reddit-summary-title-case
  severity: warn
- description: All Reddit API operations must include descriptions explaining the endpoint behavior, required scopes, and response format.
  given: $.paths[*][get,post,put,delete,patch]
  name: reddit-operation-description
  severity: warn
- description: Reddit listing endpoints use after/before fullname-based pagination rather than page numbers. List endpoints should document pagination.
  given: $.paths[*][get]
  name: reddit-pagination-params
  severity: info
- description: The subreddit path parameter must be of type string as subreddit names are alphanumeric strings.
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'subreddit')].schema
  name: reddit-subreddit-param-type
  severity: warn
- description: GET operations must define response schemas to document the structure of Reddit Thing and Listing objects.
  given: $.paths[*][get].responses[200].content.application/json
  name: reddit-response-schema
  severity: warn
- description: All Reddit API endpoints must define a 401 Unauthorized response since all endpoints require valid OAuth 2.0 tokens.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: reddit-401-response
  severity: warn
- description: All operations must include tags to organize the Reddit API by functional area (Account, Subreddits, Links and Comments, etc.).
  given: $.paths[*][get,post,put,delete,patch]
  name: reddit-tags-required
  severity: warn
- description: Authenticated Reddit API endpoints must use oauth.reddit.com as the base server URL. Public endpoints may use www.reddit.com.
  given: $.servers[0]
  name: reddit-server-url
  severity: error
rules_file: rules/reddit-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reddit/refs/heads/main/rules/reddit-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 8
slug: reddit-rules
source_filename: reddit-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Reddit API uses OAuth 2.0 - require oauth2 security scheme\n  reddit-oauth2-security:\n    description: >-\n      All Reddit API operations must use OAuth 2.0 authentication. The\n      oauth2 security scheme must be defined with authorizationCode flow\n      pointing to reddit.com authorization endpoints.\n    severity: error\n    given: $.components.securitySchemes.oauth2.flows.authorizationCode\n    then:\n      field: tokenUrl\n      function: pattern\n      functionOptions:\n        match: \"reddit.com\"\n\n  # User-Agent header is required for Reddit API\n  reddit-user-agent-required:\n    description: >-\n      Reddit API requires a descriptive User-Agent header identifying the\n      application. This must be documented in the API info or parameters.\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: pattern\n      functionOptions:\n        match: \"User-Agent\"\n\n  # API must specify rate\
  \ limits\n  reddit-rate-limits-documented:\n    description: >-\n      Reddit API has strict rate limits (60 req/min for authenticated, 1 req/sec\n      for Ads API). Rate limits must be documented in the API description.\n    severity: warn\n    given: $.info.description\n    then:\n      function: pattern\n      functionOptions:\n        match: \"rate limit|requests per\"\n\n  # Operation IDs required\n  reddit-operation-id-required:\n    description: >-\n      All Reddit API operations must have operationIds for SDK generation\n      and tooling support.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  # Summary must use Title Case\n  reddit-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case formatting following Reddit API\n      documentation conventions.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 &/'-]+$\"\n\n  # Operations need descriptions\n  reddit-operation-description:\n    description: >-\n      All Reddit API operations must include descriptions explaining the\n      endpoint behavior, required scopes, and response format.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  # Reddit API pagination uses after/before\n  reddit-pagination-params:\n    description: >-\n      Reddit listing endpoints use after/before fullname-based pagination\n      rather than page numbers. List endpoints should document pagination.\n    severity: info\n    given: $.paths[*][get]\n    then:\n      function: truthy\n\n  # Subreddit path parameter is string type\n  reddit-subreddit-param-type:\n    description: >-\n      The subreddit path parameter must be of type string as subreddit\n      names are alphanumeric strings.\n    severity: warn\n\
  \    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'subreddit')].schema\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\n  # Response schemas needed for 200 responses\n  reddit-response-schema:\n    description: >-\n      GET operations must define response schemas to document the structure\n      of Reddit Thing and Listing objects.\n    severity: warn\n    given: $.paths[*][get].responses[200].content.application/json\n    then:\n      field: schema\n      function: truthy\n\n  # 401 responses defined\n  reddit-401-response:\n    description: >-\n      All Reddit API endpoints must define a 401 Unauthorized response\n      since all endpoints require valid OAuth 2.0 tokens.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      field: '401'\n      function: truthy\n\n  # Tags organize the Reddit API\n  reddit-tags-required:\n    description: >-\n      All operations\
  \ must include tags to organize the Reddit API by\n      functional area (Account, Subreddits, Links and Comments, etc.).\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  # Server URL must use oauth.reddit.com\n  reddit-server-url:\n    description: >-\n      Authenticated Reddit API endpoints must use oauth.reddit.com as the\n      base server URL. Public endpoints may use www.reddit.com.\n    severity: error\n    given: $.servers[0]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"reddit.com\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reddit/refs/heads/main/rules/reddit-rules.yml
tags:
- Advertising
- Communities
- Content
- Social Media
- Social News
- Spectral
- Linting
- API Governance
---
