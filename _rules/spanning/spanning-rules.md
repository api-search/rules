---
api_specs:
- filename: spanning-google-workspace-api-openapi.yml
  format: yaml
  label: Spanning Backup for Google Workspace API
  slug: spanning-google-workspace-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spanning/refs/heads/main/openapi/spanning-google-workspace-api-openapi.yml
categories:
- spanning
description: Spectral linting rules defining API design standards and conventions for Spanning.
layout: rules
name: Spanning API Rules
provider_name: Spanning
provider_slug: spanning
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spanning-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: spanning-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spanning-tags-title-case
  severity: warn
- description: All operations must specify security requirements
  given: $.paths[*][*]
  name: spanning-operations-require-security
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: spanning-response-must-have-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: spanning-schema-properties-have-descriptions
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: spanning-servers-must-be-https
  severity: error
- description: Spanning APIs use API key authentication
  given: $.components.securitySchemes[*]
  name: spanning-security-scheme-is-api-key
  severity: info
rules_file: rules/spanning-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spanning/refs/heads/main/rules/spanning-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 5
slug: spanning-rules
source_filename: spanning-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  spanning-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9-]*)(\\\\s[A-Z][a-z0-9-]*)*$\"\n\n  spanning-operation-id-camel-case:\n    description: All operationIds must use camelCase\n    message: OperationId \"{{value}}\" must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spanning-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9-]*)(\\\\s[A-Z][a-z0-9-]*)*$\"\n\n  spanning-operations-require-security:\n\
  \    description: All operations must specify security requirements\n    message: Operation must define security requirements\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  spanning-response-must-have-description:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spanning-schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    message: Schema property \"{{path}}\" should have a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spanning-servers-must-be-https:\n    description: All server URLs must use HTTPS\n    message: Server URL \"{{value}}\" must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  spanning-security-scheme-is-api-key:\n    description: Spanning APIs use API key authentication\n    message: Security scheme should be apiKey type\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - apiKey\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spanning/refs/heads/main/rules/spanning-rules.yml
tags:
- Data Protection
- SaaS Backup
- Cloud Backup
- Microsoft 365
- Google Workspace
- Salesforce
- Spectral
- Linting
- API Governance
---
