---
api_specs:
- filename: runsignup-openapi.yml
  format: yaml
  label: RunSignup API
  slug: runsignup
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runsignup/refs/heads/main/openapi/runsignup-openapi.yml
categories:
- runsignup
description: Spectral linting rules defining API design standards and conventions for RunSignup.
layout: rules
name: RunSignup API Rules
provider_name: RunSignup
provider_slug: runsignup
rule_count: 16
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: runsignup-operation-id-required
  severity: error
- description: RunSignup operationIds use camelCase convention (e.g., getRaces, postRaceResults, getBibChipAssignments). This ensures consistent SDK method naming.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: runsignup-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: runsignup-tags-required
  severity: error
- description: Tags must use Title Case (e.g., "Races", "Participants", "Results")
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: runsignup-tags-title-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: runsignup-summary-required
  severity: error
- description: Operation summaries must use Title Case to match RunSignup documentation conventions (e.g., "Get Races", "Post Race Results", "Get Bib and Chip Assignments").
  given: $.paths[*][get,post,put,patch,delete].summary
  name: runsignup-summary-title-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: runsignup-description-required
  severity: warn
- description: All paths containing {race_id} must define the race_id parameter as required. RunSignup organizes all race-specific resources under the race_id path parameter.
  given: $.paths[~/race_id~][*].parameters[?(@.name == 'race_id')]
  name: runsignup-race-id-path-param-required
  severity: error
- description: Authenticated endpoints must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: runsignup-responses-must-include-401
  severity: warn
- description: GET operations must define a 200 success response
  given: $.paths[*].get.responses
  name: runsignup-get-must-return-200
  severity: error
- description: POST operations must define a 200 success response
  given: $.paths[*].post.responses
  name: runsignup-post-must-return-200
  severity: warn
- description: RunSignup API supports json and xml response formats via a ?format= query parameter. GET endpoints should document this parameter.
  given: $.paths[*].get.parameters[?(@.name == 'format')].schema.enum
  name: runsignup-format-query-param
  severity: info
- description: 'RunSignup uses consistent pagination parameters: page (integer, default 1) and results_per_page (integer, max 1000). List endpoints should document these.'
  given: $.paths[*].get.parameters[?(@.name == 'page')].schema
  name: runsignup-pagination-params-consistent
  severity: info
- description: All schema properties should define a type
  given: $.components.schemas[*].properties[*]
  name: runsignup-schema-properties-typed
  severity: warn
- description: RunSignup API paths use snake_case and hyphens for resource names (e.g., /race/{race_id}/get-bib-chip, /delete-participants). Paths should not use camelCase segments.
  given: $.paths
  name: runsignup-path-uses-kebab-case
  severity: info
- description: At least one server must be defined
  given: $
  name: runsignup-servers-defined
  severity: error
rules_file: rules/runsignup-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/runsignup/refs/heads/main/rules/runsignup-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 3
  warn: 7
slug: runsignup-rules
source_filename: runsignup-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  runsignup-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  runsignup-operation-id-camel-case:\n    description: >-\n      RunSignup operationIds use camelCase convention (e.g., getRaces, postRaceResults,\n      getBibChipAssignments). This ensures consistent SDK method naming.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  runsignup-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  runsignup-tags-title-case:\n    description: Tags must use Title Case (e.g., \"Races\", \"Participants\"\
  , \"Results\")\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  runsignup-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  runsignup-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case to match RunSignup documentation conventions\n      (e.g., \"Get Races\", \"Post Race Results\", \"Get Bib and Chip Assignments\").\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  runsignup-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n\
  \    then:\n      field: description\n      function: truthy\n\n  runsignup-race-id-path-param-required:\n    description: >-\n      All paths containing {race_id} must define the race_id parameter as required.\n      RunSignup organizes all race-specific resources under the race_id path parameter.\n    severity: error\n    given: \"$.paths[~/race_id~][*].parameters[?(@.name == 'race_id')]\"\n    then:\n      field: required\n      function: truthy\n\n  runsignup-responses-must-include-401:\n    description: Authenticated endpoints must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  runsignup-get-must-return-200:\n    description: GET operations must define a 200 success response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  runsignup-post-must-return-200:\n    description: POST\
  \ operations must define a 200 success response\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  runsignup-format-query-param:\n    description: >-\n      RunSignup API supports json and xml response formats via a ?format= query\n      parameter. GET endpoints should document this parameter.\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.name == 'format')].schema.enum\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: \"json\"\n\n  runsignup-pagination-params-consistent:\n    description: >-\n      RunSignup uses consistent pagination parameters: page (integer, default 1)\n      and results_per_page (integer, max 1000). List endpoints should document these.\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.name == 'page')].schema\"\n    then:\n      field: type\n      function: enumeration\n\
  \      functionOptions:\n        values:\n          - integer\n\n  runsignup-schema-properties-typed:\n    description: All schema properties should define a type\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  runsignup-path-uses-kebab-case:\n    description: >-\n      RunSignup API paths use snake_case and hyphens for resource names\n      (e.g., /race/{race_id}/get-bib-chip, /delete-participants). Paths\n      should not use camelCase segments.\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z]\"\n\n  runsignup-servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/runsignup/refs/heads/main/rules/runsignup-rules.yml
tags:
- Race Registration
- Event Management
- Running
- Sports
- Fitness
- Timing
- Fundraising
- Spectral
- Linting
- API Governance
---
