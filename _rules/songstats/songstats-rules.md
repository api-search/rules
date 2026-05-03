---
api_specs:
- filename: songstats-openapi.yml
  format: yaml
  label: Songstats Enterprise API
  slug: songstats-enterprise-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/songstats/refs/heads/main/openapi/songstats-openapi.yml
categories:
- songstats
description: Spectral linting rules defining API design standards and conventions for Songstats.
layout: rules
name: Songstats API Rules
provider_name: Songstats
provider_slug: songstats
rule_count: 7
rules:
- description: ''
  given: $.paths[*][*].parameters[?(@.in == 'query')].name
  name: songstats-query-param-snake-case
  severity: warn
- description: ''
  given: $.paths[*][*].summary
  name: songstats-operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: songstats-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: songstats-operation-tags-required
  severity: warn
- description: ''
  given: $.components.securitySchemes
  name: songstats-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,delete,patch].responses
  name: songstats-success-response-required
  severity: warn
- description: ''
  given: $.components.securitySchemes[?(@.type == 'apiKey')].name
  name: songstats-api-key-header-name
  severity: warn
rules_file: rules/songstats-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/songstats/refs/heads/main/rules/songstats-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: songstats-rules
source_filename: songstats-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Songstats API uses snake_case for query parameters\n  songstats-query-param-snake-case:\n    message: \"Query parameters should use snake_case\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # All operation summaries should use Title Case\n  songstats-operation-summary-title-case:\n    message: \"Operation summaries should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations should have an operationId\n  songstats-operation-id-required:\n    message: \"Operations must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Operations must have at least one tag\n\
  \  songstats-operation-tags-required:\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # API must define security schemes\n  songstats-security-schemes-defined:\n    message: \"API must define security schemes (apikey in header)\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  # Responses must document at least a 2xx response\n  songstats-success-response-required:\n    message: \"Operations must document at least one success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # API key auth should use 'apikey' header name\n  songstats-api-key-header-name:\n\
  \    message: \"API key should use 'apikey' as the header name\"\n    severity: warn\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^apikey$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/songstats/refs/heads/main/rules/songstats-rules.yml
tags:
- Analytics
- Music
- Streaming
- Artists
- Tracks
- Labels
- Spectral
- Linting
- API Governance
---
