---
api_specs:
- filename: telefoon-voice-openapi.yml
  format: yaml
  label: Telefoon Voice API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefoon/refs/heads/main/openapi/telefoon-voice-openapi.yml
- filename: telefoon-sms-openapi.yml
  format: yaml
  label: Telefoon SMS API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefoon/refs/heads/main/openapi/telefoon-sms-openapi.yml
- filename: telefoon-numbers-openapi.yml
  format: yaml
  label: Telefoon Number Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telefoon/refs/heads/main/openapi/telefoon-numbers-openapi.yml
categories:
- telefoon
description: Spectral linting rules defining API design standards and conventions for Telefoon.
layout: rules
name: Telefoon API Rules
provider_name: Telefoon
provider_slug: telefoon
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telefoon-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telefoon-operation-must-have-operationid
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: telefoon-operationid-camelcase
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: telefoon-operation-must-have-description
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: telefoon-operation-must-have-tag
  severity: warn
- description: GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: telefoon-response-200-required
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: telefoon-delete-204-response
  severity: warn
- description: API server must use EU data center domain
  given: $.servers[*].url
  name: telefoon-eu-server-required
  severity: warn
- description: API must define servers
  given: $
  name: telefoon-servers-required
  severity: error
rules_file: rules/telefoon-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telefoon/refs/heads/main/rules/telefoon-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: telefoon-rules
source_filename: telefoon-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  telefoon-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  telefoon-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  telefoon-operationid-camelcase:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telefoon-operation-must-have-description:\n    description: All operations should have a description\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  telefoon-operation-must-have-tag:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telefoon-response-200-required:\n    description: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  telefoon-delete-204-response:\n    description: DELETE operations should return 204\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  telefoon-eu-server-required:\n    description: API server must use EU data center domain\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.telefoon\\\\.com\"\n\n  telefoon-servers-required:\n    description: API must define servers\n    severity: error\n    given:\
  \ \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telefoon/refs/heads/main/rules/telefoon-rules.yml
tags:
- Belgium
- CPaaS
- EU Data Residency
- Europe
- GDPR Compliant
- Messaging
- Netherlands
- Number Provisioning
- SMS
- Telephony
- Voice
- Spectral
- Linting
- API Governance
---
