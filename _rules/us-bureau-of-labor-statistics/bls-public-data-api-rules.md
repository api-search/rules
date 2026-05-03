---
api_specs:
- filename: bls-public-data-api-openapi.yml
  format: yaml
  label: BLS Public Data API
  slug: bls-public-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bureau-of-labor-statistics/refs/heads/main/openapi/bls-public-data-api-openapi.yml
categories:
- bls
description: Spectral linting rules defining API design standards and conventions for US Bureau of Labor Statistics.
layout: rules
name: US Bureau of Labor Statistics API Rules
provider_name: US Bureau of Labor Statistics
provider_slug: us-bureau-of-labor-statistics
rule_count: 10
rules:
- description: BLS API specs must include contact information
  given: $.info
  name: bls-info-contact
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: bls-operation-tags
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: bls-operation-summary
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: bls-operation-id
  severity: error
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: bls-parameter-description
  severity: warn
- description: All 200 responses must have a schema
  given: $.paths[*][get,post,put,patch,delete].responses.200
  name: bls-response-schema
  severity: warn
- description: Registration key parameters should follow BLS naming convention
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')]
  name: bls-registration-key-pattern
  severity: info
- description: Series ID path parameters should follow BLS naming conventions
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'seriesId')]
  name: bls-series-id-format
  severity: info
- description: BLS API should return JSON responses
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content
  name: bls-json-responses
  severity: warn
- description: BLS API servers should specify versioned paths
  given: $.servers[*]
  name: bls-version-servers
  severity: info
rules_file: rules/bls-public-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-bureau-of-labor-statistics/refs/heads/main/rules/bls-public-data-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 5
slug: bls-public-data-api-rules
source_filename: bls-public-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  bls-info-contact:\n    description: BLS API specs must include contact information\n    message: \"Contact information is required in info object\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  bls-operation-tags:\n    description: All operations must be tagged\n    message: \"Operation '{{property}}' must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  bls-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation '{{property}}' must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  bls-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: operationId\n      function: truthy\n\n  bls-parameter-description:\n    description: All parameters must have a description\n    message: \"Parameter '{{value}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  bls-response-schema:\n    description: All 200 responses must have a schema\n    message: \"200 response must have content with schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  bls-registration-key-pattern:\n    description: Registration key parameters should follow BLS naming convention\n    message: \"Registration key query parameter should be named 'registrationkey'\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query')]\"\n    then:\n      function: pattern\n    \
  \  functionOptions:\n        match: \"^(registrationkey|seriesid|startyear|endyear|catalog|calculations|annualaverage|aspects|survey|latest)$\"\n      field: name\n\n  bls-series-id-format:\n    description: Series ID path parameters should follow BLS naming conventions\n    message: \"Series ID path parameter should have a pattern describing BLS format\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'seriesId')]\"\n    then:\n      field: schema.pattern\n      function: truthy\n\n  bls-json-responses:\n    description: BLS API should return JSON responses\n    message: \"Responses must include application/json content type\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content\"\n    then:\n      field: application/json\n      function: truthy\n\n  bls-version-servers:\n    description: BLS API servers should specify versioned paths\n    message: \"Server URL should include API version path\
  \ segment\"\n    severity: info\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"v[12]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-bureau-of-labor-statistics/refs/heads/main/rules/bls-public-data-api-rules.yml
tags:
- Federal Government
- Labor Statistics
- Economic Data
- Open Data
- Spectral
- Linting
- API Governance
---
