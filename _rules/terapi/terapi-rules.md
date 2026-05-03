---
api_specs:
- filename: terapi-openapi.yml
  format: yaml
  label: Terapi API
  slug: terapi-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/terapi/refs/heads/main/openapi/terapi-openapi.yml
categories:
- terapi
description: Spectral linting rules defining API design standards and conventions for Terapi.
layout: rules
name: Terapi API Rules
provider_name: Terapi
provider_slug: terapi
rule_count: 20
rules:
- description: Terapi API must use API key (secret key) authentication
  given: $
  name: terapi-security-apikey
  severity: error
- description: Terapi API paths use noun-based resource names
  given: $.paths[*]~
  name: terapi-path-resource-style
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: terapi-path-no-trailing-slash
  severity: warn
- description: List operations should use GET method
  given: $.paths[*][get].operationId
  name: terapi-list-get-method
  severity: warn
- description: Create operations should use POST
  given: $.paths[*][post].operationId
  name: terapi-create-post-method
  severity: warn
- description: Delete operations must use DELETE
  given: $.paths[*][delete].operationId
  name: terapi-delete-method
  severity: error
- description: GET operations must return 200
  given: $.paths[*][get].responses
  name: terapi-get-200-response
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*][delete].responses
  name: terapi-delete-204-response
  severity: warn
- description: All authenticated operations must define 401
  given: $.paths[*][get,post,put,patch,delete].responses
  name: terapi-401-response
  severity: error
- description: Resource operations with ID parameters should define 404
  given: $.paths[*~'/{[^}]+}'][get,delete].responses
  name: terapi-404-for-resource
  severity: warn
- description: Operations using provider_config_key should mark it required
  given: $.paths[*][*].parameters[?(@.name == 'provider_config_key')]
  name: terapi-provider-config-key-required
  severity: warn
- description: Path parameter connection_id must be required
  given: $.paths[*][*].parameters[?(@.name == 'connection_id' && @.in == 'path')]
  name: terapi-connection-id-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: terapi-operation-id
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: terapi-operation-summary
  severity: error
- description: Summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: terapi-summary-title-case
  severity: warn
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: terapi-operation-description
  severity: warn
- description: Operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: terapi-tags
  severity: error
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: terapi-schema-descriptions
  severity: warn
- description: Connection IDs should always be string type
  given: $.components.schemas[*].properties.id
  name: terapi-connection-id-string
  severity: warn
- description: Action trigger input should be an object
  given: $.components.schemas.TriggerActionRequest.properties.input
  name: terapi-input-object
  severity: warn
rules_file: rules/terapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/terapi/refs/heads/main/rules/terapi-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 12
slug: terapi-rules
source_filename: terapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Authentication\n  terapi-security-apikey:\n    description: Terapi API must use API key (secret key) authentication\n    message: \"Terapi API must define global API key security\"\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n    severity: error\n\n  # Path Conventions\n  terapi-path-resource-style:\n    description: Terapi API paths use noun-based resource names\n    message: \"Path '{{property}}' should use resource nouns (connection, integration, sync, action, auth)\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(connection|integration|sync|action|auth)\"\n    severity: warn\n\n  terapi-path-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: \"Path '{{property}}' must not have a trailing slash\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\
  \n    severity: warn\n\n  # HTTP Methods\n  terapi-list-get-method:\n    description: List operations should use GET method\n    message: \"List operations should use GET\"\n    given: \"$.paths[*][get].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get)[A-Z]\"\n    severity: warn\n\n  terapi-create-post-method:\n    description: Create operations should use POST\n    message: \"Create/trigger operations should use POST\"\n    given: \"$.paths[*][post].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(create|trigger)[A-Z]\"\n    severity: warn\n\n  terapi-delete-method:\n    description: Delete operations must use DELETE\n    message: \"Delete operations must use DELETE\"\n    given: \"$.paths[*][delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^delete[A-Z]\"\n    severity: error\n\n  # Response Codes\n  terapi-get-200-response:\n    description:\
  \ GET operations must return 200\n    message: \"GET operations must define a 200 response\"\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n\n  terapi-delete-204-response:\n    description: DELETE operations should return 204\n    message: \"DELETE operations should return 204 No Content\"\n    given: \"$.paths[*][delete].responses\"\n    then:\n      field: \"204\"\n      function: truthy\n    severity: warn\n\n  terapi-401-response:\n    description: All authenticated operations must define 401\n    message: \"All operations must define 401 Unauthorized response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n    severity: error\n\n  terapi-404-for-resource:\n    description: Resource operations with ID parameters should define 404\n    message: \"Resource operations should define 404 Not Found\"\n    given: \"$.paths[*~'/{[^}]+}'][get,delete].responses\"\
  \n    then:\n      field: \"404\"\n      function: truthy\n    severity: warn\n\n  # Parameters\n  terapi-provider-config-key-required:\n    description: Operations using provider_config_key should mark it required\n    message: \"provider_config_key parameter should be required\"\n    given: \"$.paths[*][*].parameters[?(@.name == 'provider_config_key')]\"\n    then:\n      field: required\n      function: truthy\n    severity: warn\n\n  terapi-connection-id-required:\n    description: Path parameter connection_id must be required\n    message: \"Path parameter connection_id must be marked required\"\n    given: \"$.paths[*][*].parameters[?(@.name == 'connection_id' && @.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n    severity: error\n\n  # Documentation\n  terapi-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n\
  \      field: operationId\n      function: truthy\n    severity: error\n\n  terapi-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n    severity: error\n\n  terapi-summary-title-case:\n    description: Summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case (start with capital letter)\"\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n    severity: warn\n\n  terapi-operation-description:\n    description: Operations should have descriptions\n    message: \"Operation is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  terapi-tags:\n    description: Operations must\
  \ have tags\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n    severity: error\n\n  # Schema Conventions\n  terapi-schema-descriptions:\n    description: Schema components should have descriptions\n    message: \"Schema component '{{path}}' is missing a description\"\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  terapi-connection-id-string:\n    description: Connection IDs should always be string type\n    message: \"Connection ID fields should be type: string\"\n    given: \"$.components.schemas[*].properties.id\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n    severity: warn\n\n  # Webhook/Event Consistency\n  terapi-input-object:\n    description: Action trigger input should be an object\n    message: \"Action input should be\
  \ type: object\"\n    given: \"$.components.schemas.TriggerActionRequest.properties.input\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - object\n    severity: warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/terapi/refs/heads/main/rules/terapi-rules.yml
tags:
- Authentication
- Connectors
- Embedded iPaaS
- Integration
- Native Integrations
- Open Source
- Workflow Automation
- Spectral
- Linting
- API Governance
---
