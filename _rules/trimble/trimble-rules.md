---
api_specs:
- filename: trimble-connect-openapi.yml
  format: yaml
  label: Trimble Connect API
  slug: trimble-connect
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trimble/refs/heads/main/openapi/trimble-connect-openapi.yml
- filename: trimble-maps-openapi.yml
  format: yaml
  label: Trimble Maps API
  slug: trimble-maps
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trimble/refs/heads/main/openapi/trimble-maps-openapi.yml
categories:
- trimble
description: Spectral linting rules defining API design standards and conventions for Trimble.
layout: rules
name: Trimble API Rules
provider_name: Trimble
provider_slug: trimble
rule_count: 12
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: trimble-operation-ids-camel-case
  severity: warn
- description: Operation summaries should use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: trimble-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: trimble-operation-has-tags
  severity: error
- description: Tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: trimble-tag-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: trimble-operation-description
  severity: warn
- description: Bearer auth security scheme should be named BearerAuth
  given: $.components.securitySchemes
  name: trimble-bearer-auth-scheme
  severity: warn
- description: Successful GET responses must define a response schema
  given: $.paths[*].get.responses.200.content.application/json
  name: trimble-response-200-schema
  severity: warn
- description: Project ID path parameters must be named projectId
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]
  name: trimble-project-id-path-param
  severity: warn
- description: List operations should include pagination parameters
  given: $.paths[*].get
  name: trimble-connect-pagination-params
  severity: hint
- description: Operations should define 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: trimble-error-responses
  severity: warn
- description: Internal-only operations must not appear in public API specifications
  given: $.paths[*][get,post,put,patch,delete]
  name: trimble-no-x-internal
  severity: error
- description: API specification must include a version in info object
  given: $.info
  name: trimble-api-version-in-info
  severity: error
rules_file: rules/trimble-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trimble/refs/heads/main/rules/trimble-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 8
slug: trimble-rules
source_filename: trimble-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  trimble-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trimble-operation-summary-title-case:\n    description: Operation summaries should use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ,()\\\\-']+$\"\n\n  trimble-operation-has-tags:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: tags\n      function: truthy\n\n  trimble-tag-title-case:\n    description: Tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 \\\\-]*$\"\n\n  trimble-operation-description:\n    description: All operations should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  trimble-bearer-auth-scheme:\n    description: Bearer auth security scheme should be named BearerAuth\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            BearerAuth:\n              type: object\n\n  trimble-response-200-schema:\n    description: Successful GET responses must define a response schema\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json\"\n    then:\n      field: schema\n      function: defined\n\n  trimble-project-id-path-param:\n    description: Project\
  \ ID path parameters must be named projectId\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                pattern: \".*[Pp]roject.*[Ii]d.*\"\n          then:\n            properties:\n              name:\n                const: projectId\n\n  trimble-connect-pagination-params:\n    description: List operations should include pagination parameters\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  trimble-error-responses:\n    description: Operations should define 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n\
  \            \"401\":\n              type: object\n\n  trimble-no-x-internal:\n    description: Internal-only operations must not appear in public API specifications\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-internal\n      function: falsy\n\n  trimble-api-version-in-info:\n    description: API specification must include a version in info object\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trimble/refs/heads/main/rules/trimble-rules.yml
tags:
- Construction
- Transportation
- Geospatial
- GPS
- Mapping
- BIM
- Fleet Management
- Collaboration
- Agriculture
- Spectral
- Linting
- API Governance
---
