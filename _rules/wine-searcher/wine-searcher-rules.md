---
api_specs:
- filename: wine-searcher-openapi.yml
  format: yaml
  label: Wine-Searcher API
  slug: wine-searcher-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wine-searcher/refs/heads/main/openapi/wine-searcher-openapi.yml
categories:
- wine
description: Spectral linting rules defining API design standards and conventions for Wine-Searcher.
layout: rules
name: Wine-Searcher API Rules
provider_name: Wine-Searcher
provider_slug: wine-searcher
rule_count: 9
rules:
- description: Wine-Searcher API uses GET for all endpoints
  given: $.paths[*]
  name: wine-searcher-get-only
  severity: info
- description: All Wine-Searcher API endpoints must require api_key parameter
  given: $.paths[*].get.parameters[?(@.name=='api_key')]
  name: wine-searcher-api-key-required
  severity: error
- description: All Wine-Searcher API endpoints must require winename parameter
  given: $.paths[*].get.parameters[?(@.name=='winename')]
  name: wine-searcher-winename-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: wine-searcher-operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][*].operationId
  name: wine-searcher-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: wine-searcher-operation-tags-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: wine-searcher-summary-required
  severity: error
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: wine-searcher-schema-descriptions
  severity: warn
- description: Operations must define at least one response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: wine-searcher-success-response-required
  severity: error
rules_file: rules/wine-searcher-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wine-searcher/refs/heads/main/rules/wine-searcher-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 2
slug: wine-searcher-rules
source_filename: wine-searcher-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Wine-Searcher API uses GET for all endpoints\n  wine-searcher-get-only:\n    description: Wine-Searcher API uses GET for all endpoints\n    message: \"Wine-Searcher API endpoints should use GET method\"\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # api_key must be a required query parameter\n  wine-searcher-api-key-required:\n    description: All Wine-Searcher API endpoints must require api_key parameter\n    message: \"Operation should include required 'api_key' query parameter\"\n    severity: error\n    given: \"$.paths[*].get.parameters[?(@.name=='api_key')]\"\n    then:\n      field: required\n      function: truthy\n\n  # winename must be a required query parameter\n  wine-searcher-winename-required:\n    description: All Wine-Searcher API endpoints must require winename parameter\n    message: \"Operation should\
  \ include required 'winename' query parameter\"\n    severity: error\n    given: \"$.paths[*].get.parameters[?(@.name=='winename')]\"\n    then:\n      field: required\n      function: truthy\n\n  # Operations must have operationIds\n  wine-searcher-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # OperationIds in camelCase\n  wine-searcher-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Operations must have tags\n  wine-searcher-operation-tags-required:\n    description: All operations must have at least\
  \ one tag\n    message: \"Operation is missing tags\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summaries must be present\n  wine-searcher-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Schemas should have descriptions\n  wine-searcher-schema-descriptions:\n    description: Schema components should have descriptions\n    message: \"Schema '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Responses must be defined\n  wine-searcher-success-response-required:\n    description: Operations must define at least one response\n    message: \"Operation has no responses defined\"\n\
  \    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wine-searcher/refs/heads/main/rules/wine-searcher-rules.yml
tags:
- Data
- Marketplace
- Wine
- Prices
- Merchants
- Vintages
- Critics
- Spectral
- Linting
- API Governance
---
