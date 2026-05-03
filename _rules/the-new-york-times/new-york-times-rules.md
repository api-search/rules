---
api_specs:
- filename: new-york-times-archive-openapi-original.yml
  format: yaml
  label: The New York Times Archive API
  slug: archive-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-archive-openapi-original.yml
- filename: new-york-times-article-search-openapi-original.yml
  format: yaml
  label: The New York Times Article Search API
  slug: article-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-article-search-openapi-original.yml
- filename: new-york-times-books-openapi-original.yml
  format: yaml
  label: The New York Times Books API
  slug: books-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-books-openapi-original.yml
- filename: new-york-times-most-popular-openapi-original.yml
  format: yaml
  label: The New York Times Most Popular API
  slug: most-popular
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-most-popular-openapi-original.yml
- filename: new-york-times-movie-review-openapi-original.yml
  format: yaml
  label: The New York Times Movie Reviews API
  slug: movie-reviews-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-movie-review-openapi-original.yml
- filename: new-york-times-semantic-openapi-original.yml
  format: yaml
  label: The New York Times Semantic API
  slug: semantic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-semantic-openapi-original.yml
- filename: new-york-times-times-tags-openapi-original.yml
  format: yaml
  label: The New York Times TimesTags API
  slug: timestags-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-times-tags-openapi-original.yml
- filename: new-york-times-times-newswire-openapi-original.yml
  format: yaml
  label: The New York Times Times Newswire API
  slug: times-newswire-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-times-newswire-openapi-original.yml
- filename: new-york-times-top-stories-openapi-original.yml
  format: yaml
  label: The New York Times Top Stories API
  slug: top-stories
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/openapi/new-york-times-top-stories-openapi-original.yml
categories:
- nyt
description: Spectral linting rules defining API design standards and conventions for The New York Times.
layout: rules
name: The New York Times API Rules
provider_name: The New York Times
provider_slug: the-new-york-times
rule_count: 12
rules:
- description: All NYT API operations must reference an apiKey security scheme named api-key or apikey.
  given: $.paths.*.*
  name: nyt-api-key-security-scheme
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths.*.*.summary
  name: nyt-operation-summary-title-case
  severity: warn
- description: All NYT API operations must have a summary field.
  given: $.paths.*.*
  name: nyt-operation-summary-exists
  severity: error
- description: All NYT API operations must have at least one tag.
  given: $.paths.*.*
  name: nyt-operation-tags-exist
  severity: warn
- description: All NYT API operations must define a 200 success response.
  given: $.paths.*.*.responses
  name: nyt-response-200-exists
  severity: error
- description: 200 responses should return application/json content.
  given: $.paths.*.*.responses.200.content
  name: nyt-response-json-content
  severity: warn
- description: NYT API paths must end with the .json format suffix.
  given: $.paths
  name: nyt-path-json-suffix
  severity: hint
- description: API info title must be set.
  given: $.info
  name: nyt-info-title-exists
  severity: error
- description: API info description should describe the API.
  given: $.info
  name: nyt-info-description-exists
  severity: warn
- description: NYT API server URLs should use HTTPS.
  given: $.servers[*].url
  name: nyt-server-https
  severity: warn
- description: All parameters should include a description.
  given: $.paths.*.*.parameters[*]
  name: nyt-parameter-description-exists
  severity: warn
- description: Reusable schemas should be defined under components/schemas.
  given: $.components.schemas
  name: nyt-components-schemas-reuse
  severity: hint
rules_file: rules/new-york-times-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/rules/new-york-times-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 7
slug: new-york-times-rules
source_filename: new-york-times-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # NYT APIs use api-key as a query parameter — enforce that security scheme exists\n  nyt-api-key-security-scheme:\n    description: All NYT API operations must reference an apiKey security scheme named api-key or apikey.\n    message: \"Operation must use the NYT api-key security scheme.\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: security\n\n  # NYT summaries must use Title Case\n  nyt-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][^a-z]*([A-Z][^A-Z]*)*\"\n\n  # All operations should have a summary\n  nyt-operation-summary-exists:\n    description: All NYT API operations must have a summary field.\n    message: \"Operation is missing a summary.\"\
  \n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: summary\n\n  # All operations should have tags\n  nyt-operation-tags-exist:\n    description: All NYT API operations must have at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      function: truthy\n      field: tags\n\n  # Responses must include a 200 response\n  nyt-response-200-exists:\n    description: All NYT API operations must define a 200 success response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths.*.*.responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  # Responses must include application/json content type\n  nyt-response-json-content:\n    description: 200 responses should return application/json content.\n    message: \"200 response should include application/json content type.\"\n    severity: warn\n    given: \"\
  $.paths.*.*.responses.200.content\"\n    then:\n      function: truthy\n      field: \"application/json\"\n\n  # Paths must end with .json suffix (NYT convention)\n  nyt-path-json-suffix:\n    description: NYT API paths must end with the .json format suffix.\n    message: \"Path '{{value}}' must end with .json or a format path parameter.\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*(\\\\.json|\\\\{format\\\\}).*\"\n\n  # Info title must be set\n  nyt-info-title-exists:\n    description: API info title must be set.\n    message: \"API info.title is required.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      function: truthy\n      field: title\n\n  # Info description must be set\n  nyt-info-description-exists:\n    description: API info description should describe the API.\n    message: \"API info.description is recommended.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      function:\
  \ truthy\n      field: description\n\n  # Server URLs should use HTTPS\n  nyt-server-https:\n    description: NYT API server URLs should use HTTPS.\n    message: \"Server URL '{{value}}' should use HTTPS.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Parameters must have descriptions\n  nyt-parameter-description-exists:\n    description: All parameters should include a description.\n    message: \"Parameter '{{value}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths.*.*.parameters[*]\"\n    then:\n      function: truthy\n      field: description\n\n  # Components schemas should exist when inline schemas are complex\n  nyt-components-schemas-reuse:\n    description: Reusable schemas should be defined under components/schemas.\n    message: \"Consider moving complex inline schemas to components/schemas for reuse.\"\n    severity: hint\n    given: \"$.components.schemas\"\
  \n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-new-york-times/refs/heads/main/rules/new-york-times-rules.yml
tags:
- Articles
- Books
- Movies
- News
- Media
- Publishing
- Journalism
- Spectral
- Linting
- API Governance
---
