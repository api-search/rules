---
api_specs:
- filename: supermicro-redfish-openapi.yml
  format: yaml
  label: Supermicro Redfish API
  slug: redfish-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/super-micro-computer/refs/heads/main/openapi/supermicro-redfish-openapi.yml
categories:
- supermicro
description: Spectral linting rules defining API design standards and conventions for Super Micro Computer.
layout: rules
name: Super Micro Computer API Rules
provider_name: Super Micro Computer
provider_slug: super-micro-computer
rule_count: 10
rules:
- description: All Supermicro Redfish resources must include @odata.type
  given: $.paths[*][get].responses[200].content.application/json.schema.properties
  name: supermicro-odata-type-required
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: supermicro-operation-id-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: supermicro-summary-title-case
  severity: warn
- description: All Supermicro Redfish paths should be nested under /redfish/v1
  given: $.servers[*].url
  name: supermicro-redfish-path-prefix
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: supermicro-tags-required
  severity: warn
- description: All path parameters must have a description
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: supermicro-path-parameters-described
  severity: warn
- description: Security schemes must include BasicAuth and SessionAuth
  given: $.components.securitySchemes
  name: supermicro-security-defined
  severity: error
- description: Reset action paths should include ActionResponse in their response schema
  given: $.paths[*Actions*][post].responses
  name: supermicro-reset-action-typed
  severity: warn
- description: Status objects should use the defined Status schema
  given: $.components.schemas.*.properties.Status
  name: supermicro-status-schema-health
  severity: warn
- description: Collection responses must include Members@odata.count
  given: $.components.schemas.Collection.properties
  name: supermicro-collection-members-count
  severity: error
rules_file: rules/supermicro-redfish-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/super-micro-computer/refs/heads/main/rules/supermicro-redfish-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: supermicro-redfish-rules
source_filename: supermicro-redfish-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  supermicro-odata-type-required:\n    description: All Supermicro Redfish resources must include @odata.type\n    severity: error\n    given: $.paths[*][get].responses[200].content.application/json.schema.properties\n    then:\n      field: '@odata.type'\n      function: truthy\n\n  supermicro-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: truthy\n\n  supermicro-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: $.paths[*][*].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$'\n\n  supermicro-redfish-path-prefix:\n    description: All Supermicro Redfish paths should be nested under /redfish/v1\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: '/redfish/v[0-9]+'\n\n  supermicro-tags-required:\n    description: All operations must have at least one tag\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: truthy\n\n  supermicro-path-parameters-described:\n    description: All path parameters must have a description\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.in == 'path')]\n    then:\n      field: description\n      function: truthy\n\n  supermicro-security-defined:\n    description: Security schemes must include BasicAuth and SessionAuth\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - BasicAuth\n            - SessionAuth\n\n  supermicro-reset-action-typed:\n    description: Reset action paths should include ActionResponse in their response schema\n    severity: warn\n    given: $.paths[*Actions*][post].responses\n    then:\n     \
  \ field: '200'\n      function: truthy\n\n  supermicro-status-schema-health:\n    description: Status objects should use the defined Status schema\n    severity: warn\n    given: $.components.schemas.*.properties.Status\n    then:\n      function: truthy\n\n  supermicro-collection-members-count:\n    description: Collection responses must include Members@odata.count\n    severity: error\n    given: $.components.schemas.Collection.properties\n    then:\n      field: 'Members@odata.count'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/super-micro-computer/refs/heads/main/rules/supermicro-redfish-rules.yml
tags:
- Servers
- Data Center
- Hardware
- Server Management
- Redfish
- BMC
- IPMI
- Fortune 500
- Infrastructure
- Cloud
- Spectral
- Linting
- API Governance
---
