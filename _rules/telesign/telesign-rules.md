---
api_specs:
- filename: telesign-sms-openapi.yml
  format: yaml
  label: Telesign SMS API
  slug: sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/openapi/telesign-sms-openapi.yml
- filename: telesign-phoneid-openapi.yml
  format: yaml
  label: Telesign PhoneID API
  slug: phoneid-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/openapi/telesign-phoneid-openapi.yml
- filename: telesign-verify-openapi.yml
  format: yaml
  label: Telesign Verify API
  slug: verify-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/openapi/telesign-verify-openapi.yml
- filename: telesign-score-openapi.yml
  format: yaml
  label: Telesign Score API
  slug: score-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/openapi/telesign-score-openapi.yml
categories:
- telesign
description: Spectral linting rules defining API design standards and conventions for Telesign.
layout: rules
name: Telesign API Rules
provider_name: Telesign
provider_slug: telesign
rule_count: 12
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telesign-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telesign-operation-must-have-operationid
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: telesign-operationid-kebab-case
  severity: warn
- description: Phone number parameters should be named 'phone_number' or 'complete_phone_number' and include country code in their description
  given: $.paths[*][*].parameters[?(@.name == 'phone_number' || @.name == 'complete_phone_number')]
  name: telesign-phone-number-parameter
  severity: hint
- description: Successful responses should include a reference_id field for transaction tracking
  given: $.paths[*].post.responses.200.content['application/json'].schema.properties
  name: telesign-reference-id-response
  severity: warn
- description: Successful responses should include a status object with code and description
  given: $.paths[*].post.responses.200.content['application/json'].schema.properties
  name: telesign-status-object-in-response
  severity: warn
- description: All paths must require BasicAuth security
  given: $.paths[*][*]
  name: telesign-requires-basic-auth
  severity: error
- description: Server URL must point to rest-ww.telesign.com
  given: $.servers[*].url
  name: telesign-server-must-be-telesign
  severity: error
- description: POST operations must handle 400 Bad Request
  given: $.paths[*].post.responses
  name: telesign-response-must-have-400
  severity: warn
- description: All operations must handle 401 Unauthorized
  given: $.paths[*][*].responses
  name: telesign-response-must-have-401
  severity: error
- description: POST operations must handle 429 rate limiting
  given: $.paths[*].post.responses
  name: telesign-response-must-have-429
  severity: warn
- description: account_lifecycle_event must use the approved enum values
  given: $.paths[*][*]..properties.account_lifecycle_event
  name: telesign-account-lifecycle-enum
  severity: warn
rules_file: rules/telesign-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/rules/telesign-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 7
slug: telesign-rules
source_filename: telesign-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  telesign-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  telesign-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  telesign-operationid-kebab-case:\n    description: Operation IDs should use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telesign-phone-number-parameter:\n    description: >-\n      Phone number parameters should be named 'phone_number' or 'complete_phone_number'\n      and include country code in their description\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.name\
  \ == 'phone_number' || @.name == 'complete_phone_number')]\"\n    then:\n      field: description\n      function: truthy\n\n  telesign-reference-id-response:\n    description: >-\n      Successful responses should include a reference_id field for transaction tracking\n    severity: warn\n    given: \"$.paths[*].post.responses.200.content['application/json'].schema.properties\"\n    then:\n      field: reference_id\n      function: truthy\n\n  telesign-status-object-in-response:\n    description: >-\n      Successful responses should include a status object with code and description\n    severity: warn\n    given: \"$.paths[*].post.responses.200.content['application/json'].schema.properties\"\n    then:\n      field: status\n      function: truthy\n\n  telesign-requires-basic-auth:\n    description: All paths must require BasicAuth security\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  telesign-server-must-be-telesign:\n\
  \    description: Server URL must point to rest-ww.telesign.com\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://rest-ww\\\\.telesign\\\\.com\"\n\n  telesign-response-must-have-400:\n    description: POST operations must handle 400 Bad Request\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: '400'\n      function: truthy\n\n  telesign-response-must-have-401:\n    description: All operations must handle 401 Unauthorized\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  telesign-response-must-have-429:\n    description: POST operations must handle 429 rate limiting\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: '429'\n      function: truthy\n\n  telesign-account-lifecycle-enum:\n    description: >-\n      account_lifecycle_event must use the approved\
  \ enum values\n    severity: warn\n    given: \"$.paths[*][*]..properties.account_lifecycle_event\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telesign/refs/heads/main/rules/telesign-rules.yml
tags:
- Authentication
- Communications
- Fraud Prevention
- Phone Intelligence
- SMS
- Verification
- Spectral
- Linting
- API Governance
---
