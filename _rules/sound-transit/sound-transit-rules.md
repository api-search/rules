---
api_specs:
- filename: sound-transit-onebusaway-openapi.yml
  format: yaml
  label: Sound Transit OneBusAway API
  slug: sound-transit-onebusaway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sound-transit/refs/heads/main/openapi/sound-transit-onebusaway-openapi.yml
categories:
- sound
description: Spectral linting rules defining API design standards and conventions for Sound Transit.
layout: rules
name: Sound Transit API Rules
provider_name: Sound Transit
provider_slug: sound-transit
rule_count: 10
rules:
- description: All Sound Transit API operations require the 'key' query parameter
  given: $.paths[*][get].parameters[?(@.name == 'key')]
  name: sound-transit-api-key-required
  severity: error
- description: Sound Transit OneBusAway API paths use .json suffix
  given: $.paths
  name: sound-transit-json-suffix
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sound-transit-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sound-transit-operation-id-required
  severity: error
- description: OperationId must use camelCase convention
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sound-transit-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sound-transit-operation-has-tags
  severity: warn
- description: Operations must document 401 Unauthorized for invalid API key
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sound-transit-401-response
  severity: warn
- description: Successful responses must have a schema
  given: $.paths[*][get].responses['200'].content['application/json']
  name: sound-transit-response-schema-defined
  severity: warn
- description: All tags in the spec must use Title Case
  given: $.tags[*].name
  name: sound-transit-tags-title-case
  severity: warn
- description: All response schemas should reference BaseResponse or include code and currentTime fields
  given: $.components.schemas.BaseResponse
  name: sound-transit-base-response-structure
  severity: info
rules_file: rules/sound-transit-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sound-transit/refs/heads/main/rules/sound-transit-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: sound-transit-rules
source_filename: sound-transit-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sound Transit OneBusAway API always requires API key query parameter\n  sound-transit-api-key-required:\n    description: All Sound Transit API operations require the 'key' query parameter\n    severity: error\n    given: \"$.paths[*][get].parameters[?(@.name == 'key')]\"\n    then:\n      field: required\n      function: truthy\n\n  # All paths use .json suffix - enforce this pattern\n  sound-transit-json-suffix:\n    description: Sound Transit OneBusAway API paths use .json suffix\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\.json$\"\n\n  # All operations must have summaries in Title Case\n  sound-transit-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([\
  \ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # All operations must have operationId\n  sound-transit-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId must use camelCase\n  sound-transit-operation-id-camel-case:\n    description: OperationId must use camelCase convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have tags\n  sound-transit-operation-has-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # 401 response for missing API key\n  sound-transit-401-response:\n    description: Operations must document\
  \ 401 Unauthorized for invalid API key\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  # Response schemas must be defined\n  sound-transit-response-schema-defined:\n    description: Successful responses must have a schema\n    severity: warn\n    given: \"$.paths[*][get].responses['200'].content['application/json']\"\n    then:\n      field: schema\n      function: defined\n\n  # All tags must be Title Case\n  sound-transit-tags-title-case:\n    description: All tags in the spec must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # BaseResponse structure - all responses inherit from BaseResponse\n  sound-transit-base-response-structure:\n    description: All response schemas should reference BaseResponse or include code and currentTime fields\n\
  \    severity: info\n    given: \"$.components.schemas.BaseResponse\"\n    then:\n      field: properties\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sound-transit/refs/heads/main/rules/sound-transit-rules.yml
tags:
- Transit
- Transportation
- GTFS
- Real-Time
- Public Transit
- Government
- Seattle
- Spectral
- Linting
- API Governance
---
