---
api_specs:
- filename: windstream-voice-openapi.yml
  format: yaml
  label: Windstream Enterprise Voice API
  slug: windstream-voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/windstream-holdings/refs/heads/main/openapi/windstream-voice-openapi.yml
- filename: windstream-contact-center-openapi.yml
  format: yaml
  label: Windstream Enterprise Contact Center Services API
  slug: windstream-contact-center-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/windstream-holdings/refs/heads/main/openapi/windstream-contact-center-openapi.yml
categories:
- windstream
description: Spectral linting rules defining API design standards and conventions for Windstream Holdings.
layout: rules
name: Windstream Holdings API Rules
provider_name: Windstream Holdings
provider_slug: windstream-holdings
rule_count: 9
rules:
- description: Tenant and extension path parameters should use UUID format
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: windstream-uuid-path-params
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: windstream-operation-id-required
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][*].operationId
  name: windstream-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: windstream-operation-tags-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: windstream-summary-required
  severity: error
- description: GET operations should not have request bodies
  given: $.paths[*].get
  name: windstream-no-get-request-body
  severity: error
- description: Operations must define at least one response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: windstream-success-response-required
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: windstream-schema-property-descriptions
  severity: info
- description: HAL responses should use application/hal+json content type
  given: $.paths[*][*].responses[*].content
  name: windstream-hal-content-type
  severity: info
rules_file: rules/windstream-holdings-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/windstream-holdings/refs/heads/main/rules/windstream-holdings-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 2
slug: windstream-holdings-rules
source_filename: windstream-holdings-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Windstream APIs use UUID path parameters for tenant/extension operations\n  windstream-uuid-path-params:\n    description: Tenant and extension path parameters should use UUID format\n    message: \"Path parameter '{{value}}' for tenant/extension should be a UUID\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # All operations must have operationIds\n  windstream-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # OperationIds use camelCase\n  windstream-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId '{{value}}'\
  \ should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Operations must have tags\n  windstream-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summaries must be present and use Title Case\n  windstream-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # GET operations should not have request bodies\n  windstream-no-get-request-body:\n    description: GET operations should not have request bodies\n    message: \"GET operation should not\
  \ have a requestBody\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # Responses must include success codes\n  windstream-success-response-required:\n    description: Operations must define at least one response\n    message: \"Operation has no responses defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  # Schema properties should have descriptions\n  windstream-schema-property-descriptions:\n    description: Schema properties should have descriptions\n    message: \"Schema property is missing a description\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # HAL responses should use application/hal+json content type\n  windstream-hal-content-type:\n  \
  \  description: HAL responses should use application/hal+json content type\n    message: \"HAL response should declare application/hal+json content type\"\n    severity: info\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/windstream-holdings/refs/heads/main/rules/windstream-holdings-rules.yml
tags:
- Broadband
- Contact Center
- Managed Services
- Network Communications
- SD-WAN
- Telecom
- UCaaS
- Unified Communications
- Spectral
- Linting
- API Governance
---
