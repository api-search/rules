---
api_specs:
- filename: tmdb-api.json
  format: json
  label: The Movie Database API
  slug: the-movie-database
  spec_type: OpenAPI
  url: https://developer.themoviedb.org/openapi/tmdb-api.json
categories:
- tmdb
description: Spectral linting rules defining API design standards and conventions for The Movie Database.
layout: rules
name: The Movie Database API Rules
provider_name: The Movie Database
provider_slug: the-movie-database
rule_count: 10
rules:
- description: All TMDB API operations must define an operationId for client SDK generation.
  given: $.paths[*][*]
  name: tmdb-operations-must-have-operationid
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: tmdb-operations-must-have-summary
  severity: warn
- description: All read operations must define a 200 success response.
  given: $.paths[*][get].responses
  name: tmdb-responses-must-include-200
  severity: error
- description: All write operations must document 401 Unauthorized.
  given: $.paths[*][post].responses
  name: tmdb-responses-must-include-401
  severity: warn
- description: The language parameter must have a description indicating ISO 639-1 format.
  given: $.paths[*][*].parameters[?(@.name == 'language')]
  name: tmdb-language-param-must-have-description
  severity: warn
- description: The page parameter must be an integer type.
  given: $.paths[*][*].parameters[?(@.name == 'page')].schema
  name: tmdb-page-param-must-be-integer
  severity: error
- description: Path parameters ending in _id (movie_id, series_id, person_id) must be integer type.
  given: $.paths[*][*].parameters[?(@.in == 'path' && @.name =~ /.*_id$/)]
  name: tmdb-path-id-params-must-be-integer
  severity: warn
- description: 200 responses must define application/json content.
  given: $.paths[*][get].responses.200
  name: tmdb-responses-define-json-content
  severity: warn
- description: The API info object should include contact information.
  given: $.info
  name: tmdb-info-must-have-contact
  severity: warn
- description: All parameters should have descriptions for clarity.
  given: $.paths[*][*].parameters[*]
  name: tmdb-parameters-must-have-descriptions
  severity: warn
rules_file: rules/the-movie-database-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-movie-database/refs/heads/main/rules/the-movie-database-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: the-movie-database-rules
source_filename: the-movie-database-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tmdb-operations-must-have-operationid:\n    description: All TMDB API operations must define an operationId for client SDK generation.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tmdb-operations-must-have-summary:\n    description: All operations must have a summary.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tmdb-responses-must-include-200:\n    description: All read operations must define a 200 success response.\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  tmdb-responses-must-include-401:\n    description: All write operations must document 401 Unauthorized.\n    severity: warn\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  tmdb-language-param-must-have-description:\n\
  \    description: The language parameter must have a description indicating ISO 639-1 format.\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'language')]\"\n    then:\n      field: description\n      function: truthy\n\n  tmdb-page-param-must-be-integer:\n    description: The page parameter must be an integer type.\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name == 'page')].schema\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  tmdb-path-id-params-must-be-integer:\n    description: Path parameters ending in _id (movie_id, series_id, person_id) must be integer type.\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path' && @.name =~ /.*_id$/)]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  tmdb-responses-define-json-content:\n    description: 200 responses\
  \ must define application/json content.\n    severity: warn\n    given: \"$.paths[*][get].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  tmdb-info-must-have-contact:\n    description: The API info object should include contact information.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  tmdb-parameters-must-have-descriptions:\n    description: All parameters should have descriptions for clarity.\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-movie-database/refs/heads/main/rules/the-movie-database-rules.yml
tags:
- Entertainment
- Movies
- Television
- Spectral
- Linting
- API Governance
---
