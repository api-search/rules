---
api_specs:
- filename: the-cat-api-openapi.yml
  format: yaml
  label: The Cat API
  slug: the-cat-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-cat-api/refs/heads/main/openapi/the-cat-api-openapi.yml
categories:
- catapi
description: Spectral linting rules defining API design standards and conventions for The Cat API.
layout: rules
name: The Cat API API Rules
provider_name: The Cat API
provider_slug: the-cat-api
rule_count: 10
rules:
- description: All Cat API operations must be tagged (Images, Breeds, Favourites, Votes, Categories).
  given: $.paths[*][*]
  name: catapi-operations-must-have-tags
  severity: warn
- description: All operations must have a summary in Title Case.
  given: $.paths[*][*]
  name: catapi-operations-must-have-summary
  severity: warn
- description: All operations must define an operationId for SDK generation.
  given: $.paths[*][*]
  name: catapi-operations-must-have-operationid
  severity: error
- description: All read operations must define a 200 success response.
  given: $.paths[*][get].responses
  name: catapi-responses-must-include-200
  severity: error
- description: All write operations should document a 401 Unauthorized response.
  given: $.paths[*][post].responses
  name: catapi-responses-must-include-401
  severity: warn
- description: All path and query parameters must have descriptions.
  given: $.paths[*][*].parameters[*]
  name: catapi-parameters-must-have-descriptions
  severity: warn
- description: Collection paths must use plural nouns (e.g., /images, /breeds, /votes, /favourites).
  given: $.paths
  name: catapi-collection-paths-use-plural-nouns
  severity: warn
- description: Path parameter names must use snake_case.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: catapi-path-parameters-use-snake-case
  severity: warn
- description: All 200 responses should define a content type.
  given: $.paths[*][get].responses.200
  name: catapi-responses-define-content-type
  severity: warn
- description: The API info object must include a version.
  given: $.info
  name: catapi-info-must-have-version
  severity: error
rules_file: rules/the-cat-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-cat-api/refs/heads/main/rules/the-cat-api-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: the-cat-api-rules
source_filename: the-cat-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  catapi-operations-must-have-tags:\n    description: All Cat API operations must be tagged (Images, Breeds, Favourites, Votes, Categories).\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  catapi-operations-must-have-summary:\n    description: All operations must have a summary in Title Case.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  catapi-operations-must-have-operationid:\n    description: All operations must define an operationId for SDK generation.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  catapi-responses-must-include-200:\n    description: All read operations must define a 200 success response.\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  catapi-responses-must-include-401:\n\
  \    description: All write operations should document a 401 Unauthorized response.\n    severity: warn\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"401\"\n      function: falsy\n\n  catapi-parameters-must-have-descriptions:\n    description: All path and query parameters must have descriptions.\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  catapi-collection-paths-use-plural-nouns:\n    description: Collection paths must use plural nouns (e.g., /images, /breeds, /votes, /favourites).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z-]+s(/|$)\"\n\n  catapi-path-parameters-use-snake-case:\n    description: Path parameter names must use snake_case.\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n\
  \        match: \"^[a-z][a-z0-9_]*$\"\n\n  catapi-responses-define-content-type:\n    description: All 200 responses should define a content type.\n    severity: warn\n    given: \"$.paths[*][get].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  catapi-info-must-have-version:\n    description: The API info object must include a version.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-cat-api/refs/heads/main/rules/the-cat-api-rules.yml
tags:
- Animals
- Cats
- Images
- Media
- Spectral
- Linting
- API Governance
---
