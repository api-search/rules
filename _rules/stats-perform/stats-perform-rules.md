---
api_specs:
- filename: stats-perform-stats-api-openapi.yml
  format: yaml
  label: STATS API
  slug: stats-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stats-perform/refs/heads/main/openapi/stats-perform-stats-api-openapi.yml
categories:
- stats
description: Spectral linting rules defining API design standards and conventions for Stats Perform.
layout: rules
name: Stats Perform API Rules
provider_name: Stats Perform
provider_slug: stats-perform
rule_count: 8
rules:
- description: Stats Perform STATS API requires an API key passed as "api_key" query parameter for all authenticated endpoints.
  given: $.paths[*][*]
  name: stats-perform-api-key-required
  severity: error
- description: 'Stats Perform paths follow a consistent structure: /stats/{sport}/{leaguePath}/... or /editorial/{sport}/{leaguePath}/... The sport path parameter must be one of the defined sport types.'
  given: $.paths[?(@ =~ /^\/stats\/|^\/editorial\//)]
  name: stats-perform-path-sport-prefix
  severity: warn
- description: Stats Perform API operation IDs use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: stats-perform-operation-ids-camel-case
  severity: warn
- description: All Stats Perform API operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: stats-perform-summaries-title-case
  severity: warn
- description: Every Stats Perform API operation must have at least one tag for proper documentation grouping.
  given: $.paths[*][*]
  name: stats-perform-tags-required
  severity: error
- description: Stats Perform API list responses typically wrap their data in an "apiResults" array. List operation responses should follow this pattern.
  given: $.paths[?(@ =~ /\/$/)]..responses['200'].content['application/json'].schema.properties
  name: stats-perform-api-results-wrapper
  severity: hint
- description: Stats Perform path segments are case-sensitive. Decode endpoint paths such as /decode/networkTypes/ use camelCase. All path segments must match the documented casing exactly.
  given: $.paths
  name: stats-perform-case-sensitive-paths
  severity: error
- description: Stats Perform uses consistent event status values across all sports.
  given: $.components.schemas[*].properties.status.enum
  name: stats-perform-event-status-values
  severity: hint
rules_file: rules/stats-perform-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stats-perform/refs/heads/main/rules/stats-perform-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 3
slug: stats-perform-rules
source_filename: stats-perform-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stats-perform-api-key-required:\n    description: >-\n      Stats Perform STATS API requires an API key passed as \"api_key\" query\n      parameter for all authenticated endpoints.\n    message: >-\n      Operations should require the \"api_key\" query parameter for\n      authentication.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: parameters\n      function: truthy\n\n  stats-perform-path-sport-prefix:\n    description: >-\n      Stats Perform paths follow a consistent structure:\n      /stats/{sport}/{leaguePath}/... or /editorial/{sport}/{leaguePath}/...\n      The sport path parameter must be one of the defined sport types.\n    message: >-\n      Paths under /stats/ or /editorial/ must include sport and leaguePath\n      template parameters.\n    severity: warn\n    given: \"$.paths[?(@ =~ /^\\\\/stats\\\\/|^\\\\/editorial\\\\//)]\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \".*\\\\{sport\\\\}.*\\\\{leaguePath\\\\}.*\"\n\n  stats-perform-operation-ids-camel-case:\n    description: >-\n      Stats Perform API operation IDs use camelCase naming convention.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  stats-perform-summaries-title-case:\n    description: >-\n      All Stats Perform API operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  stats-perform-tags-required:\n    description: >-\n      Every Stats Perform API operation must have at least one tag for\n      proper documentation grouping.\n    message: \"Operations must declare at least one tag.\"\n  \
  \  severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  stats-perform-api-results-wrapper:\n    description: >-\n      Stats Perform API list responses typically wrap their data in an\n      \"apiResults\" array. List operation responses should follow this pattern.\n    message: >-\n      List operation 200 responses should include an \"apiResults\" property\n      in the response schema.\n    severity: hint\n    given: \"$.paths[?(@ =~ /\\\\/$/)]..responses['200'].content['application/json'].schema.properties\"\n    then:\n      field: apiResults\n      function: truthy\n\n  stats-perform-case-sensitive-paths:\n    description: >-\n      Stats Perform path segments are case-sensitive. Decode endpoint paths\n      such as /decode/networkTypes/ use camelCase. All path segments must\n      match the documented casing exactly.\n    message: >-\n      Path segments are case-sensitive in the Stats Perform API. Ensure\n      correct casing\
  \ in all path segments.\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*[A-Z]{2,}.*\"\n\n  stats-perform-event-status-values:\n    description: >-\n      Stats Perform uses consistent event status values across all sports.\n    message: \"Event status should be one of: pre-event, in-progress, final, postponed, cancelled.\"\n    severity: hint\n    given: \"$.components.schemas[*].properties.status.enum\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stats-perform/refs/heads/main/rules/stats-perform-rules.yml
tags:
- Sports
- Sports Data
- Football
- Baseball
- Basketball
- Hockey
- Soccer
- Golf
- Tennis
- Live Scores
- Statistics
- Sports Analytics
- Spectral
- Linting
- API Governance
---
