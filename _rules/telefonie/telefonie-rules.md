---
api_specs:
- filename: telefonie-voice-openapi.yml
  format: yaml
  label: Telefonie Voice API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/openapi/telefonie-voice-openapi.yml
- filename: telefonie-sms-openapi.yml
  format: yaml
  label: Telefonie SMS API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/openapi/telefonie-sms-openapi.yml
- filename: telefonie-numbers-openapi.yml
  format: yaml
  label: Telefonie Number Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/openapi/telefonie-numbers-openapi.yml
- filename: telefonie-recording-openapi.yml
  format: yaml
  label: Telefonie Call Recording API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/openapi/telefonie-recording-openapi.yml
categories:
- telefonie
description: Spectral linting rules defining API design standards and conventions for Telefonie.
layout: rules
name: Telefonie API Rules
provider_name: Telefonie
provider_slug: telefonie
rule_count: 12
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telefonie-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telefonie-operation-must-have-operationid
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: telefonie-operationid-camelcase
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: telefonie-operation-must-have-description
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: telefonie-operation-must-have-tag
  severity: warn
- description: Phone number parameters should reference E.164 format in their descriptions
  given: $.paths[*][*].parameters[?(@.name == 'to' || @.name == 'from' || @.name == 'phone_number')]
  name: telefonie-phone-number-e164
  severity: info
- description: GET and POST operations must define a 200 or 201 response
  given: $.paths[*].get.responses
  name: telefonie-response-200-required
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: telefonie-delete-204-response
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: telefonie-schema-properties-have-description
  severity: info
- description: List endpoints should support page and page_size parameters
  given: $.paths[*].get.operationId
  name: telefonie-pagination-parameters
  severity: info
- description: All operations must have security defined
  given: $.paths[*][*]
  name: telefonie-security-required
  severity: error
- description: API must define servers
  given: $
  name: telefonie-servers-required
  severity: error
rules_file: rules/telefonie-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/rules/telefonie-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 4
  warn: 4
slug: telefonie-rules
source_filename: telefonie-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  telefonie-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  telefonie-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  telefonie-operationid-camelcase:\n    description: Operation IDs must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telefonie-operation-must-have-description:\n    description: All operations\
  \ should have a description\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefonie-operation-must-have-tag:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telefonie-phone-number-e164:\n    description: Phone number parameters should reference E.164 format in their descriptions\n    message: \"Phone number parameter '{{path}}' description should mention E.164 format\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'to' || @.name == 'from' || @.name == 'phone_number')]\"\n    then:\n      field: description\n      function: truthy\n\n  telefonie-response-200-required:\n    description: GET and POST operations must define a 200 or 201 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  telefonie-delete-204-response:\n\
  \    description: DELETE operations should return 204\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  telefonie-schema-properties-have-description:\n    description: Schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefonie-pagination-parameters:\n    description: List endpoints should support page and page_size parameters\n    severity: info\n    given: \"$.paths[*].get.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^list\"\n\n  telefonie-security-required:\n    description: All operations must have security defined\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: falsy\n\n  telefonie-servers-required:\n    description: API must define servers\n    severity: error\n    given:\
  \ \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telefonie/refs/heads/main/rules/telefonie-rules.yml
tags:
- Call Recording
- CPaaS
- Messaging
- Number Provisioning
- SMS
- Telecommunications
- Telephony
- Voice
- VoIP
- Spectral
- Linting
- API Governance
---
