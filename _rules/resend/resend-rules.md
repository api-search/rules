---
api_specs:
- filename: resend-openapi.yml
  format: yaml
  label: Resend API
  slug: resend
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/resend/refs/heads/main/openapi/resend-openapi.yml
categories:
- resend
description: Spectral linting rules defining API design standards and conventions for Resend.
layout: rules
name: Resend API Rules
provider_name: Resend
provider_slug: resend
rule_count: 11
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: resend-operation-id
  severity: error
- description: All operations must have a summary in Title Case.
  given: $.paths[*][get,post,put,patch,delete]
  name: resend-operation-summary
  severity: error
- description: All operations should use Bearer token authentication.
  given: $.paths[*][*]
  name: resend-bearer-auth
  severity: warn
- description: All operations should have a 200 or 201 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: resend-response-200-or-201
  severity: error
- description: POST operations that create resources should have a request body.
  given: $.paths[*].post
  name: resend-request-body-post
  severity: warn
- description: Path parameters for resource IDs should use snake_case with _id suffix.
  given: $.paths[*].parameters[?(@.in == 'path')]
  name: resend-path-resource-id
  severity: info
- description: Collection paths should use plural nouns.
  given: $.paths[?(!@property.match(/{.*}/))][*]~
  name: resend-path-plural-nouns
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: resend-tags-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: resend-operation-tags
  severity: warn
- description: Success responses should reference a schema.
  given: $.paths[*][*].responses[200,201].content.application/json.schema
  name: resend-response-schema
  severity: warn
- description: API should document rate limiting behavior.
  given: $.info
  name: resend-rate-limit-documented
  severity: info
rules_file: rules/resend-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/resend/refs/heads/main/rules/resend-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 6
slug: resend-rules
source_filename: resend-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  resend-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  resend-operation-summary:\n    description: All operations must have a summary in Title Case.\n    message: Operation is missing a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  resend-bearer-auth:\n    description: All operations should use Bearer token authentication.\n    message: Operation should reference bearerAuth security scheme.\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: security\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  resend-response-200-or-201:\n    description: All operations should have a 200 or 201 success response.\n\
  \    message: Operation should define a success response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  resend-request-body-post:\n    description: POST operations that create resources should have a request body.\n    message: POST operation should include a request body.\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n\n  resend-path-resource-id:\n    description: Path parameters for resource IDs should use snake_case with _id suffix.\n    message: Resource ID parameter should follow snake_case _id naming pattern.\n    severity: info\n    given: $.paths[*].parameters[?(@.in == 'path')]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  resend-path-plural-nouns:\n\
  \    description: Collection paths should use plural nouns.\n    message: Collection endpoint path should use a plural noun.\n    severity: warn\n    given: $.paths[?(!@property.match(/{.*}/))][*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^\\/(emails|domains|api-keys|audiences|broadcasts)'\n\n  resend-tags-title-case:\n    description: All tags must use Title Case.\n    message: Tag name should use Title Case.\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z ]*$'\n\n  resend-operation-tags:\n    description: All operations must have at least one tag.\n    message: Operation is missing tags.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  resend-response-schema:\n    description: Success responses should reference a schema.\n    message: Success response should include a schema.\n   \
  \ severity: warn\n    given: $.paths[*][*].responses[200,201].content.application/json.schema\n    then:\n      function: truthy\n\n  resend-rate-limit-documented:\n    description: API should document rate limiting behavior.\n    message: API info should reference rate limiting documentation.\n    severity: info\n    given: $.info\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/resend/refs/heads/main/rules/resend-rules.yml
tags:
- Email
- Developer Tools
- Transactional Email
- Marketing Email
- Spectral
- Linting
- API Governance
---
