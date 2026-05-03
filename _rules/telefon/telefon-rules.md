---
api_specs:
- filename: telefon-voice-openapi.yml
  format: yaml
  label: Telefon Voice API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/openapi/telefon-voice-openapi.yml
- filename: telefon-sms-openapi.yml
  format: yaml
  label: Telefon SMS API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/openapi/telefon-sms-openapi.yml
- filename: telefon-numbers-openapi.yml
  format: yaml
  label: Telefon Number Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/openapi/telefon-numbers-openapi.yml
- filename: telefon-recording-openapi.yml
  format: yaml
  label: Telefon Call Recording API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/openapi/telefon-recording-openapi.yml
categories:
- telefon
description: Spectral linting rules defining API design standards and conventions for Telefon.
layout: rules
name: Telefon API Rules
provider_name: Telefon
provider_slug: telefon
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telefon-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telefon-operation-must-have-operationid
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: telefon-operationid-camelcase
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: telefon-operation-must-have-description
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: telefon-operation-must-have-tag
  severity: warn
- description: GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: telefon-response-200-required
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: telefon-delete-204-response
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: telefon-schema-properties-have-description
  severity: info
- description: API must define servers
  given: $
  name: telefon-servers-required
  severity: error
rules_file: rules/telefon-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/rules/telefon-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 4
slug: telefon-rules
source_filename: telefon-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  telefon-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  telefon-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  telefon-operationid-camelcase:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telefon-operation-must-have-description:\n    description: All operations should have a description\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  telefon-operation-must-have-tag:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telefon-response-200-required:\n    description: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  telefon-delete-204-response:\n    description: DELETE operations should return 204\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  telefon-schema-properties-have-description:\n    description: Schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  telefon-servers-required:\n    description: API must define servers\n    severity: error\n    given: \"$\"\n    then:\n\
  \      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telefon/refs/heads/main/rules/telefon-rules.yml
tags:
- Call Recording
- Communications
- CPaaS
- Global Coverage
- Messaging
- Number Provisioning
- SMS
- Telephony
- Voice
- VoIP
- Spectral
- Linting
- API Governance
---
