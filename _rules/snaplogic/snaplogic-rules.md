---
api_specs:
- filename: snaplogic-public-apis-openapi.yml
  format: yaml
  label: SnapLogic Public APIs
  slug: snaplogic-public-apis
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snaplogic/refs/heads/main/openapi/snaplogic-public-apis-openapi.yml
categories:
- snaplogic
description: Spectral linting rules defining API design standards and conventions for SnapLogic.
layout: rules
name: SnapLogic API Rules
provider_name: SnapLogic
provider_slug: snaplogic
rule_count: 8
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][*].operationId
  name: snaplogic-operation-id-camel-case
  severity: warn
- description: All SnapLogic API operations must define security (JWT or Basic Auth)
  given: $.paths[*][get,post,put,delete,patch]
  name: snaplogic-security-defined
  severity: error
- description: All operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: snaplogic-operation-tag
  severity: warn
- description: All operations must have a summary in Title Case
  given: $.paths[*][get,post,put,delete,patch]
  name: snaplogic-operation-summary
  severity: warn
- description: All operations should have a detailed description
  given: $.paths[*][get,post,put,delete,patch]
  name: snaplogic-operation-description
  severity: info
- description: All successful responses should define a schema
  given: $.paths[*][*].responses['200'].content
  name: snaplogic-success-response-schema
  severity: warn
- description: All path parameters must be defined in the parameters section
  given: $.paths[*][*].parameters[*][?(@.in == 'path')]
  name: snaplogic-path-params-defined
  severity: error
- description: Server URLs should include org variable for multi-tenant support
  given: $.servers[*].url
  name: snaplogic-server-variables
  severity: info
rules_file: rules/snaplogic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/snaplogic/refs/heads/main/rules/snaplogic-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: snaplogic-rules
source_filename: snaplogic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation naming\n  snaplogic-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: \"operationId '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Auth requirements\n  snaplogic-security-defined:\n    description: All SnapLogic API operations must define security (JWT or Basic Auth)\n    message: \"Operation must define security requirements (JWT bearer or Basic Auth)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: security\n      function: truthy\n\n  # Tag requirements\n  snaplogic-operation-tag:\n    description: All operations must have at least one tag for grouping\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # Summary requirements\n  snaplogic-operation-summary:\n    description: All operations must have a summary in Title Case\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Description requirements\n  snaplogic-operation-description:\n    description: All operations should have a detailed description\n    message: \"Operation should have a description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  # Response schema\n  snaplogic-success-response-schema:\n    description: All successful responses should define a schema\n    message: \"200/201 response should have a defined schema\"\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content\"\n    then:\n      function: truthy\n\n  # Path parameter\
  \ consistency\n  snaplogic-path-params-defined:\n    description: All path parameters must be defined in the parameters section\n    message: \"Path parameters must be defined\"\n    severity: error\n    given: \"$.paths[*][*].parameters[*][?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  # Server variables\n  snaplogic-server-variables:\n    description: Server URLs should include org variable for multi-tenant support\n    message: \"Server URL should include {org} variable for SnapLogic multi-tenancy\"\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{org\\\\}.*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/snaplogic/refs/heads/main/rules/snaplogic-rules.yml
tags:
- AI
- API Management
- Automation
- Data Integration
- Integrations
- iPaaS
- Management
- Spectral
- Linting
- API Governance
---
