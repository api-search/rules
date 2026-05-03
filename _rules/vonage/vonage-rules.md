---
api_specs:
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage SMS API
  slug: vonage-sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage Voice API
  slug: vonage-voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage Messages API
  slug: vonage-messages-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage Verify API
  slug: vonage-verify-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage Numbers API
  slug: vonage-numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
- filename: vonage-openapi.yml
  format: yaml
  label: Vonage Application API
  slug: vonage-application-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/openapi/vonage-openapi.yml
categories:
- vonage
description: Spectral linting rules defining API design standards and conventions for Vonage.
layout: rules
name: Vonage API Rules
provider_name: Vonage
provider_slug: vonage
rule_count: 11
rules:
- description: Operation IDs must use camelCase.
  given: $.paths[*][*].operationId
  name: vonage-operation-ids-camel-case
  severity: warn
- description: Tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: vonage-tags-title-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: vonage-operation-summary-required
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: vonage-operation-tags-required
  severity: warn
- description: GET operations must define a 200 response.
  given: $.paths[*].get
  name: vonage-response-200-defined
  severity: warn
- description: POST create operations should return 201.
  given: $.paths[*].post
  name: vonage-response-201-post
  severity: info
- description: Vonage REST API (rest.nexmo.com) uses api_key and api_secret in request body. Ensure these are documented as required fields.
  given: $.paths[/sms/json,/account/numbers,/number/search,/number/buy,/number/cancel,/number/update][post,get].requestBody.content[*].schema.required
  name: vonage-api-key-secret-in-body
  severity: info
- description: Voice API operations must use Bearer JWT authentication.
  given: $.paths[/v1/calls,/v1/calls/*][*].security[*]
  name: vonage-bearer-auth-voice
  severity: info
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: vonage-description-required
  severity: info
- description: API paths should use kebab-case segments.
  given: $.paths
  name: vonage-path-kebab-case
  severity: info
- description: All parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: vonage-parameters-described
  severity: info
rules_file: rules/vonage-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/rules/vonage-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 6
  warn: 4
slug: vonage-rules
source_filename: vonage-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vonage-operation-ids-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vonage-tags-title-case:\n    description: Tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 \\\\-]*$\"\n\n  vonage-operation-summary-required:\n    description: All operations must have a summary.\n    message: \"Operation must have a summary.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  vonage-operation-tags-required:\n    description: All operations must have\
  \ at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  vonage-response-200-defined:\n    description: GET operations must define a 200 response.\n    message: \"GET operation must define a 200 response.\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  vonage-response-201-post:\n    description: POST create operations should return 201.\n    message: \"POST create operations should return 201.\"\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.201\n      function: defined\n\n  vonage-api-key-secret-in-body:\n    description: >-\n      Vonage REST API (rest.nexmo.com) uses api_key and api_secret in request body.\n      Ensure these are documented as required fields.\n    message: \"api_key and api_secret should be documented as\
  \ required for legacy REST endpoints.\"\n    severity: info\n    given: \"$.paths[/sms/json,/account/numbers,/number/search,/number/buy,/number/cancel,/number/update][post,get].requestBody.content[*].schema.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: string\n            enum: [api_key]\n\n  vonage-bearer-auth-voice:\n    description: Voice API operations must use Bearer JWT authentication.\n    message: \"Voice API operations should use Bearer JWT auth.\"\n    severity: info\n    given: \"$.paths[/v1/calls,/v1/calls/*][*].security[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [bearerAuth]\n\n  vonage-description-required:\n    description: All operations should have a description.\n    message: \"Operation should have a description.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: description\n      function: defined\n\n  vonage-path-kebab-case:\n    description: API paths should use kebab-case segments.\n    message: \"Path '{{path}}' should use kebab-case.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}\\\\-._~]*)*$\"\n\n  vonage-parameters-described:\n    description: All parameters should have descriptions.\n    message: \"Parameter '{{value}}' should have a description.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vonage/refs/heads/main/rules/vonage-rules.yml
tags:
- Communication
- Messaging
- Telecommunications
- Video Conferencing
- Voice
- SMS
- Verification
- Spectral
- Linting
- API Governance
---
