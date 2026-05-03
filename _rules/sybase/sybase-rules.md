---
api_specs:
- filename: sybase-ase-rest-api-openapi.yml
  format: yaml
  label: Sybase ASE REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sybase/refs/heads/main/openapi/sybase-ase-rest-api-openapi.yml
- filename: openapi.json
  format: json
  label: Sybase IQ REST API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sybase.example.com/iq/v1/openapi.json
categories:
- sybase
description: Spectral linting rules defining API design standards and conventions for Sybase.
layout: rules
name: Sybase API Rules
provider_name: Sybase
provider_slug: sybase
rule_count: 8
rules:
- description: All resource paths should be under /servers/{serverId}
  given: $.paths
  name: sybase-server-path-prefix
  severity: hint
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][get,post,put,patch,delete]
  name: sybase-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sybase-summary-title-case
  severity: warn
- description: POST operations that create resources should return 201 Created
  given: $.paths[*].post.responses
  name: sybase-create-returns-201
  severity: warn
- description: serverId path parameter must be marked as required
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'serverId')]
  name: sybase-server-id-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sybase-operation-tags
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sybase-auth-response
  severity: warn
- description: Operations must have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: sybase-operation-description
  severity: warn
rules_file: rules/sybase-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sybase/refs/heads/main/rules/sybase-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 6
slug: sybase-rules
source_filename: sybase-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n  # Sybase ASE REST API uses /servers/{serverId} hierarchical path pattern\n  sybase-server-path-prefix:\n    description: All resource paths should be under /servers/{serverId}\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # Operation IDs must use camelCase\n  sybase-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Summaries must use Title Case\n  sybase-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # POST operations creating resources should return 201\n  sybase-create-returns-201:\n    description: POST operations that create resources should return 201 Created\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['201']\n            - required: ['202']\n\n  # serverId path parameter must be required\n  sybase-server-id-required:\n    description: serverId path parameter must be marked as required\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'serverId')]\"\n    then:\n      field: required\n      function: truthy\n\n  # All operations must have at least one tag\n  sybase-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n\
  \      function: truthy\n\n  # 401 response must be defined for all operations\n  sybase-auth-response:\n    description: All operations must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  # Descriptions should be present on all operations\n  sybase-operation-description:\n    description: Operations must have descriptions\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sybase/refs/heads/main/rules/sybase-rules.yml
tags:
- Database
- Enterprise
- SAP
- SQL
- Spectral
- Linting
- API Governance
---
