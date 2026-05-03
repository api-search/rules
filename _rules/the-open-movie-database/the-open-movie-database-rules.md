---
api_specs:
- filename: the-open-movie-database-openapi.yml
  format: yaml
  label: The Open Movie Database API
  slug: the-open-movie-database
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-open-movie-database/refs/heads/main/openapi/the-open-movie-database-openapi.yml
categories:
- omdb
description: Spectral linting rules defining API design standards and conventions for The Open Movie Database.
layout: rules
name: The Open Movie Database API Rules
provider_name: The Open Movie Database
provider_slug: the-open-movie-database
rule_count: 9
rules:
- description: All operations must require the apiKey query parameter security scheme.
  given: $.paths[*][get,post,put,delete,patch]
  name: omdb-api-key-security
  severity: error
- description: Every operation must have a non-empty summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: omdb-operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: omdb-title-case-summary
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: omdb-operation-tags
  severity: warn
- description: Every operation must define a 200 response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: omdb-200-response
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: omdb-https-servers
  severity: error
- description: All parameters must include a description.
  given: $.paths[*][*].parameters[*]
  name: omdb-parameter-descriptions
  severity: warn
- description: All schema objects in components should have a description.
  given: $.components.schemas[*]
  name: omdb-schema-descriptions
  severity: info
- description: Every operation must define an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: omdb-operation-id
  severity: error
rules_file: rules/the-open-movie-database-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-open-movie-database/refs/heads/main/rules/the-open-movie-database-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 3
slug: the-open-movie-database-rules
source_filename: the-open-movie-database-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  omdb-api-key-security:\n    description: All operations must require the apiKey query parameter security scheme.\n    message: \"Operation '{{operationId}}' is missing apiKey security requirement.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      - field: security\n        function: truthy\n\n  omdb-operation-summary:\n    description: Every operation must have a non-empty summary.\n    message: \"Operation '{{operationId}}' is missing a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      - field: summary\n        function: truthy\n\n  omdb-title-case-summary:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][^a-z]*([A-Z][^A-Z]*)*\"\n\
  \n  omdb-operation-tags:\n    description: Every operation must have at least one tag.\n    message: \"Operation '{{operationId}}' must include at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      - field: tags\n        function: truthy\n\n  omdb-200-response:\n    description: Every operation must define a 200 response.\n    message: \"Operation '{{operationId}}' is missing a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      - field: \"200\"\n        function: truthy\n\n  omdb-https-servers:\n    description: All server URLs must use HTTPS.\n    message: \"Server URL '{{value}}' must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  omdb-parameter-descriptions:\n    description: All parameters must include a description.\n    message: \"Parameter '{{value}}'\
  \ is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      - field: description\n        function: truthy\n\n  omdb-schema-descriptions:\n    description: All schema objects in components should have a description.\n    message: \"Schema '{{path}}' is missing a description.\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      - field: description\n        function: truthy\n\n  omdb-operation-id:\n    description: Every operation must define an operationId.\n    message: \"Operation at '{{path}}' is missing an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      - field: operationId\n        function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-open-movie-database/refs/heads/main/rules/the-open-movie-database-rules.yml
tags:
- Entertainment
- Movies
- Television
- IMDb
- Metadata
- Spectral
- Linting
- API Governance
---
