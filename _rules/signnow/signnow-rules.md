---
api_specs:
- filename: signnow-openapi.yml
  format: yaml
  label: SignNow REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/signnow/refs/heads/main/openapi/signnow-openapi.yml
categories:
- signnow
description: Spectral linting rules defining API design standards and conventions for SignNow.
layout: rules
name: SignNow API Rules
provider_name: SignNow
provider_slug: signnow
rule_count: 9
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: signnow-operation-summary-title-case
  severity: warn
- description: Operation IDs should use camelCase consistent with SignNow conventions.
  given: $.paths[*][*].operationId
  name: signnow-operation-ids-kebab
  severity: warn
- description: All operations (except authentication) must require BearerAuth security.
  given: $.paths[?(!@property.match(/oauth2/))][*]
  name: signnow-bearer-auth-required
  severity: warn
- description: Document ID path parameters should be named document_id.
  given: $.paths./document/{document_id}[*].parameters[*]
  name: signnow-document-id-path-param
  severity: info
- description: Error responses must reference the Error schema.
  given: $.paths[*][*].responses[?(@property >= '400')].content['application/json'].schema
  name: signnow-error-schema-defined
  severity: warn
- description: All successful operations must define a 200 response.
  given: $.paths[*][*].responses
  name: signnow-response-200-defined
  severity: error
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: signnow-tags-defined
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][*]
  name: signnow-description-present
  severity: warn
- description: API paths must not be empty.
  given: $.paths[*]
  name: signnow-no-empty-paths
  severity: error
rules_file: rules/signnow-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/signnow/refs/heads/main/rules/signnow-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: signnow-rules
source_filename: signnow-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  signnow-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: 'Summary \"{{value}}\" must use Title Case.'\n    severity: warn\n    given: '$.paths[*][*].summary'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-z]+(\\s[A-Z][a-z]+)*$'\n\n  signnow-operation-ids-kebab:\n    description: Operation IDs should use camelCase consistent with SignNow conventions.\n    message: 'OperationId \"{{value}}\" should be camelCase.'\n    severity: warn\n    given: '$.paths[*][*].operationId'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  signnow-bearer-auth-required:\n    description: All operations (except authentication) must require BearerAuth security.\n    message: Operation must declare security requirements.\n    severity: warn\n    given: '$.paths[?(!@property.match(/oauth2/))][*]'\n    then:\n      field:\
  \ security\n      function: defined\n\n  signnow-document-id-path-param:\n    description: Document ID path parameters should be named document_id.\n    message: 'Document ID path parameters should be named \"document_id\".'\n    severity: info\n    given: '$.paths./document/{document_id}[*].parameters[*]'\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n        - document_id\n\n  signnow-error-schema-defined:\n    description: Error responses must reference the Error schema.\n    message: Error responses (4xx/5xx) must reference the Error schema component.\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '400')].content['application/json'].schema\"\n    then:\n      function: defined\n\n  signnow-response-200-defined:\n    description: All successful operations must define a 200 response.\n    message: Operation must define a 200 success response.\n    severity: error\n    given: '$.paths[*][*].responses'\n  \
  \  then:\n      field: '200'\n      function: defined\n\n  signnow-tags-defined:\n    description: All operations must include at least one tag.\n    message: Operation must include at least one tag for categorization.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: tags\n      function: defined\n\n  signnow-description-present:\n    description: All operations must have a description.\n    message: Operation must include a description.\n    severity: warn\n    given: '$.paths[*][*]'\n    then:\n      field: description\n      function: defined\n\n  signnow-no-empty-paths:\n    description: API paths must not be empty.\n    message: Path must define at least one operation.\n    severity: error\n    given: '$.paths[*]'\n    then:\n      function: length\n      functionOptions:\n        min: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/signnow/refs/heads/main/rules/signnow-rules.yml
tags:
- E-Signature
- Document Management
- Electronic Signature
- Workflow Automation
- Spectral
- Linting
- API Governance
---
