---
api_specs:
- filename: regal-cinema-openapi.yml
  format: yaml
  label: Regal Cinema API
  slug: regal-cinema-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/regal-entertainment-group/refs/heads/main/openapi/regal-cinema-openapi.yml
categories:
- regal
description: Spectral linting rules defining API design standards and conventions for regal-entertainment-group.
layout: rules
name: regal-entertainment-group API Rules
provider_name: regal-entertainment-group
provider_slug: regal-entertainment-group
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: regal-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: regal-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: regal-paths-kebab-case
  severity: warn
- description: All paths must be prefixed with /v1/
  given: $.paths
  name: regal-v1-prefix
  severity: warn
- description: All operations must require the ApiKeyAuth security scheme
  given: $.paths[*][*]
  name: regal-requires-api-key-security
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: regal-operations-have-summaries
  severity: error
- description: Successful GET responses must define a schema
  given: $.paths[*].get.responses.200.content[*]
  name: regal-response-200-has-schema
  severity: warn
- description: Error responses must reference the Error schema
  given: $.paths[*][*].responses[?(@property >= '400')].content[*]
  name: regal-error-schema-defined
  severity: warn
rules_file: rules/regal-cinema-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/regal-entertainment-group/refs/heads/main/rules/regal-cinema-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: regal-cinema-rules
source_filename: regal-cinema-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  regal-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"{{property}} must be camelCase (e.g., listMovies, getTheatre)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  regal-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  regal-paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment in '{{property}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/(\\\\{[a-zA-Z]+\\\\}|[a-z][a-z0-9-]*))*)*$\"\n\n  regal-v1-prefix:\n\
  \    description: All paths must be prefixed with /v1/\n    message: \"Path '{{property}}' must be prefixed with /v1/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  regal-requires-api-key-security:\n    description: All operations must require the ApiKeyAuth security scheme\n    message: \"Operation '{{property}}' must use ApiKeyAuth security\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  regal-operations-have-summaries:\n    description: All operations must have a summary\n    message: \"Operation '{{property}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  regal-response-200-has-schema:\n    description: Successful GET responses must define a schema\n    message: \"GET operation '{{property}}' 200 response must define a schema\"\n    severity:\
  \ warn\n    given: \"$.paths[*].get.responses.200.content[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  regal-error-schema-defined:\n    description: Error responses must reference the Error schema\n    message: \"Error response must include a schema\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '400')].content[*]\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/regal-entertainment-group/refs/heads/main/rules/regal-cinema-rules.yml
tags:
- Cinema
- Entertainment
- Movies
- Ticketing
- Loyalty
- Theatre
- Fortune 500
- Spectral
- Linting
- API Governance
---
