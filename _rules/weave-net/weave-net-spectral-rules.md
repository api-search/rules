---
api_specs:
- filename: weave-net-openapi.yml
  format: yaml
  label: Weave Net HTTP API
  slug: weave-net-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weave-net/refs/heads/main/openapi/weave-net-openapi.yml
categories:
- delete
- get
- info
- openapi
- operation
- parameter
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Weave Net.
layout: rules
name: Weave Net API Rules
provider_name: Weave Net
provider_slug: weave-net
rule_count: 22
rules:
- description: Info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info should have contact information
  given: $.info
  name: info-contact-recommended
  severity: info
- description: Info should have license information
  given: $.info
  name: info-license-required
  severity: warn
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers must be defined
  given: $
  name: servers-required
  severity: error
- description: Server entries should have descriptions
  given: $.servers[*]
  name: servers-description-required
  severity: info
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-operationId-camel-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: warn
- description: Operation summaries must start with 'Weave Net'
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-weave-net-prefix
  severity: info
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Parameters must have a schema
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Every operation must have a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204 or 200
  given: $.paths[*].delete.responses
  name: delete-returns-correct-status
  severity: info
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-described
  severity: info
- description: Operations should have x-microcks-operation for mock support
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-microcks-extension
  severity: info
rules_file: rules/weave-net-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/weave-net/refs/heads/main/rules/weave-net-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 6
  warn: 8
slug: weave-net-spectral-rules
source_filename: weave-net-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: Info must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-recommended:\n    description: Info should have contact information\n    severity: info\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-license-required:\n    description: Info should have license information\n    severity: warn\n    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: Must use OpenAPI 3.x\n    severity:\
  \ error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-description-required:\n    description: Server entries should have descriptions\n    severity: info\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # OPERATIONS\n  operation-operationId-required:\n    description: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camel-case:\n    description: OperationIds must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\
  \n\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-weave-net-prefix:\n    description: Operation summaries must start with 'Weave Net'\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Weave Net\"\n\n  operation-description-required:\n    description: Operations should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Operations must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Parameters\
  \ should have descriptions\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: Parameters must have a schema\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have a success response\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          minProperties: 1\n\n  response-description-required:\n    description: Every response must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET\
  \ operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-returns-correct-status:\n    description: DELETE operations should return 204 or 200\n    severity: info\n    given: $.paths[*].delete.responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['204']\n            - required: ['200']\n\n  # SCHEMAS\n  schema-properties-described:\n    description: Schema properties should have descriptions\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  # MICROCKS EXTENSIONS\n  operation-microcks-extension:\n    description: Operations should have x-microcks-operation for mock support\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/weave-net/refs/heads/main/rules/weave-net-spectral-rules.yml
tags:
- Containers
- Networking
- Kubernetes
- Docker
- IPAM
- Open Source
- CNCF
- Spectral
- Linting
- API Governance
---
