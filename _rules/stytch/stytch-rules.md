---
api_specs:
- filename: stytch-consumer-openapi.yml
  format: yaml
  label: Stytch Consumer Authentication API
  slug: stytch-consumer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stytch/refs/heads/main/openapi/stytch-consumer-openapi.yml
- filename: stytch-b2b-openapi.yml
  format: yaml
  label: Stytch B2B Authentication API
  slug: stytch-b2b-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stytch/refs/heads/main/openapi/stytch-b2b-openapi.yml
categories:
- stytch
description: Spectral linting rules defining API design standards and conventions for Stytch.
layout: rules
name: Stytch API Rules
provider_name: Stytch
provider_slug: stytch
rule_count: 9
rules:
- description: All Stytch API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: stytch-operation-id-required
  severity: error
- description: Stytch operationIds use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: stytch-operation-id-camel-case
  severity: warn
- description: All operations must include at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: stytch-tags-required
  severity: warn
- description: Stytch APIs use Basic auth (project_id + secret)
  given: $.components.securitySchemes
  name: stytch-auth-basic
  severity: error
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: stytch-response-200
  severity: warn
- description: API must define servers including test and production
  given: $
  name: stytch-servers-defined
  severity: error
- description: POST operations should define a requestBody
  given: $.paths[*].post
  name: stytch-request-body-for-post
  severity: warn
- description: API paths must not end with a trailing slash
  given: $.paths[*]~
  name: stytch-no-trailing-slash
  severity: warn
- description: Operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: stytch-description-required
  severity: hint
rules_file: rules/stytch-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stytch/refs/heads/main/rules/stytch-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 5
slug: stytch-rules
source_filename: stytch-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stytch-operation-id-required:\n    description: All Stytch API operations must have an operationId\n    message: \"Operation at '{{path}}' is missing operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  stytch-operation-id-camel-case:\n    description: Stytch operationIds use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  stytch-tags-required:\n    description: All operations must include at least one tag\n    message: \"Operation '{{path}}' must include tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  stytch-auth-basic:\n    description:\
  \ Stytch APIs use Basic auth (project_id + secret)\n    message: \"API must define basicAuth security scheme\"\n    given: \"$.components.securitySchemes\"\n    severity: error\n    then:\n      field: basicAuth\n      function: truthy\n\n  stytch-response-200:\n    description: All operations must define a 200 response\n    message: \"Operation must define a 200 response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    severity: warn\n    then:\n      field: \"200\"\n      function: truthy\n\n  stytch-servers-defined:\n    description: API must define servers including test and production\n    message: \"API must define servers\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n\n  stytch-request-body-for-post:\n    description: POST operations should define a requestBody\n    message: \"POST operation at '{{path}}' should include a requestBody\"\n    given: \"$.paths[*].post\"\n    severity: warn\n    then:\n     \
  \ field: requestBody\n      function: truthy\n\n  stytch-no-trailing-slash:\n    description: API paths must not end with a trailing slash\n    message: \"Path '{{property}}' must not end with /\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  stytch-description-required:\n    description: Operations should have a description\n    message: \"Operation at '{{path}}' should have a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: hint\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stytch/refs/heads/main/rules/stytch-rules.yml
tags:
- Authentication
- Identity
- Passwordless
- Security
- Developer Tools
- Spectral
- Linting
- API Governance
---
