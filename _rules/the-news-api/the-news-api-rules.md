---
api_specs:
- filename: the-news-api-openapi.yml
  format: yaml
  label: The News API
  slug: the-news-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-news-api/refs/heads/main/openapi/the-news-api-openapi.yml
categories:
- news
description: Spectral linting rules defining API design standards and conventions for The News API.
layout: rules
name: The News API API Rules
provider_name: The News API
provider_slug: the-news-api
rule_count: 9
rules:
- description: All News API operations must include the api_token query parameter.
  given: $.paths.*.*.parameters
  name: news-api-token-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: news-api-summary-title-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths.*.*
  name: news-api-summary-exists
  severity: error
- description: All operations must have at least one tag.
  given: $.paths.*.*
  name: news-api-tags-exist
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths.*.*.responses
  name: news-api-response-200
  severity: error
- description: Server URLs should use HTTPS.
  given: $.servers[*].url
  name: news-api-server-https
  severity: warn
- description: All parameters should include a description.
  given: $.paths.*.*.parameters[*]
  name: news-api-parameter-descriptions
  severity: warn
- description: Operations should define a 401 Unauthorized response.
  given: $.paths.*.*.responses
  name: news-api-response-401
  severity: hint
- description: operationId should use camelCase.
  given: $.paths.*.*.operationId
  name: news-api-operation-id-camel-case
  severity: hint
rules_file: rules/the-news-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-news-api/refs/heads/main/rules/the-news-api-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 4
slug: the-news-api-rules
source_filename: the-news-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All operations must have api_token parameter\n  news-api-token-required:\n    description: All News API operations must include the api_token query parameter.\n    message: \"Operation must include the api_token authentication parameter.\"\n    severity: error\n    given: \"$.paths.*.*.parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: api_token\n\n  # Summaries must use Title Case\n  news-api-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary should use Title Case.\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations must have summaries\n  news-api-summary-exists:\n    description: All operations must\
  \ have a summary.\n    message: \"Operation is missing a summary.\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: summary\n\n  # All operations must have tags\n  news-api-tags-exist:\n    description: All operations must have at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: tags\n\n  # 200 responses must exist\n  news-api-response-200:\n    description: All operations must define a 200 response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths.*.*.responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  # Server URLs should use HTTPS\n  news-api-server-https:\n    description: Server URLs should use HTTPS.\n    message: \"Server URL should use HTTPS.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n    \
  \  functionOptions:\n        match: \"^https://\"\n\n  # Path parameters must have descriptions\n  news-api-parameter-descriptions:\n    description: All parameters should include a description.\n    message: \"Parameter is missing a description.\"\n    severity: warn\n    given: \"$.paths.*.*.parameters[*]\"\n    then:\n      function: truthy\n      field: description\n\n  # 401 response should be defined for secured endpoints\n  news-api-response-401:\n    description: Operations should define a 401 Unauthorized response.\n    message: \"Consider defining a 401 response for authentication failure.\"\n    severity: hint\n    given: \"$.paths.*.*.responses\"\n    then:\n      function: truthy\n      field: \"401\"\n\n  # operationIds must be camelCase\n  news-api-operation-id-camel-case:\n    description: operationId should use camelCase.\n    message: \"operationId '{{value}}' should use camelCase.\"\n    severity: hint\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-news-api/refs/heads/main/rules/the-news-api-rules.yml
tags:
- Articles
- Headlines
- News
- Media
- Search
- International
- Spectral
- Linting
- API Governance
---
