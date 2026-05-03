---
categories:
- scalar
description: Spectral linting rules defining API design standards and conventions for Scalar.
layout: rules
name: Scalar API Rules
provider_name: Scalar
provider_slug: scalar
rule_count: 16
rules:
- description: API title must be present and non-empty.
  given: $.info
  name: scalar-info-title
  severity: error
- description: API description should provide meaningful context.
  given: $.info
  name: scalar-info-description
  severity: warn
- description: API version must follow semver (major.minor.patch).
  given: $.info.version
  name: scalar-info-version
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: scalar-operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete][summary]
  name: scalar-operation-summary-title-case
  severity: warn
- description: Every operation must have a unique operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: scalar-operation-operationid
  severity: error
- description: operationId should use camelCase or kebab-case.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: scalar-operation-operationid-kebab
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: scalar-operation-tags
  severity: warn
- description: All path segments must use lowercase kebab-case.
  given: $.paths[*]~
  name: scalar-path-kebab-case
  severity: warn
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: scalar-no-trailing-slash
  severity: warn
- description: Every operation must define at least one response.
  given: $.paths[*][get,post,put,patch,delete]
  name: scalar-operation-responses
  severity: error
- description: GET operations should define a 200 response.
  given: $.paths[*].get
  name: scalar-operation-success-response
  severity: warn
- description: All named schema components should have descriptions.
  given: $.components.schemas[*]
  name: scalar-schema-description
  severity: warn
- description: All parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: scalar-parameter-description
  severity: warn
- description: If security is used in operations, securitySchemes must be defined.
  given: $
  name: scalar-security-schemes-defined
  severity: warn
- description: At least one server must be defined.
  given: $
  name: scalar-servers-present
  severity: warn
rules_file: rules/scalar-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scalar/refs/heads/main/rules/scalar-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 12
slug: scalar-rules
source_filename: scalar-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Info section completeness\n  scalar-info-title:\n    description: API title must be present and non-empty.\n    message: \"{{description}}: {{error}}\"\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  scalar-info-description:\n    description: API description should provide meaningful context.\n    message: \"{{description}}: {{error}}\"\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  scalar-info-version:\n    description: API version must follow semver (major.minor.patch).\n    message: \"{{description}}: {{error}}\"\n    severity: warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\d+\\\\.\\\\d+\\\\.\\\\d+$\"\n\n  # Operation conventions\n  scalar-operation-summary:\n    description: Every operation must have a summary.\n    message: \"Operation {{path}} is missing\
  \ a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  scalar-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete][summary]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*(\\\\s[A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  scalar-operation-operationid:\n    description: Every operation must have a unique operationId.\n    message: \"Operation {{path}} is missing an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  scalar-operation-operationid-kebab:\n    description: operationId should use camelCase or kebab-case.\n    message: \"operationId '{{value}}' should use\
  \ camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  scalar-operation-tags:\n    description: Every operation must have at least one tag.\n    message: \"Operation {{path}} must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Path conventions\n  scalar-path-kebab-case:\n    description: All path segments must use lowercase kebab-case.\n    message: \"Path '{{path}}' must use lowercase kebab-case segments.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*$\"\n\n  scalar-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n    message: \"Path '{{value}}' must not have a trailing\
  \ slash.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # Response conventions\n  scalar-operation-responses:\n    description: Every operation must define at least one response.\n    message: \"Operation {{path}} must define at least one response.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses\n      function: truthy\n\n  scalar-operation-success-response:\n    description: GET operations should define a 200 response.\n    message: \"GET operation at {{path}} should have a 200 response.\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: \"responses.200\"\n      function: truthy\n\n  # Components / schema conventions\n  scalar-schema-description:\n    description: All named schema components should have descriptions.\n    message: \"Schema '{{path}}' is missing a description.\"\n    severity: warn\n   \
  \ given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  scalar-parameter-description:\n    description: All parameters should have descriptions.\n    message: \"Parameter '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Security\n  scalar-security-schemes-defined:\n    description: If security is used in operations, securitySchemes must be defined.\n    message: \"securitySchemes must be defined in components when security is applied.\"\n    severity: warn\n    given: \"$\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            required: [\"security\"]\n          then:\n            required: [\"components\"]\n            properties:\n              components:\n                required: [\"securitySchemes\"]\n\n  # Servers\n  scalar-servers-present:\n    description: At least\
  \ one server must be defined.\n    message: \"OpenAPI document should define at least one server.\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scalar/refs/heads/main/rules/scalar-rules.yml
tags:
- API Client
- API Documentation
- API References
- Code Generation
- Developer Tools
- OpenAPI
- Registry
- SDKs
- Swagger
- Spectral
- Linting
- API Governance
---
