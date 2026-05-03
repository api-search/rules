---
api_specs:
- filename: veryfi-ocr-openapi.yml
  format: yaml
  label: Veryfi OCR API
  slug: ocr-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veryfi/refs/heads/main/openapi/veryfi-ocr-openapi.yml
categories:
- veryfi
description: Spectral linting rules defining API design standards and conventions for Veryfi.
layout: rules
name: Veryfi API Rules
provider_name: Veryfi
provider_slug: veryfi
rule_count: 10
rules:
- description: Operation IDs must use camelCase as per Veryfi API conventions
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: veryfi-operation-ids-camel-case
  severity: warn
- description: All paths must be under /partner/ namespace
  given: $.paths[*]~
  name: veryfi-paths-must-use-partner-prefix
  severity: warn
- description: All operations must declare clientId security
  given: $.paths[*][get,post,put,patch,delete]
  name: veryfi-require-client-id-security
  severity: error
- description: Document creation endpoints must return 201 Created
  given: $.paths[*].post.responses
  name: veryfi-document-responses-must-be-201
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: veryfi-require-operation-description
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: veryfi-require-operation-tags
  severity: warn
- description: Error responses must include a schema
  given: $.paths[*][get,post,put,patch,delete].responses['4*','5*'].content['application/json']
  name: veryfi-error-responses-must-reference-schema
  severity: warn
- description: API info must include contact information
  given: $.info
  name: veryfi-require-api-contact
  severity: info
- description: Document IDs in paths must be integers
  given: $.paths[*][get,delete].parameters[?(@.name == 'documentId')].schema
  name: veryfi-document-id-must-be-integer
  severity: warn
- description: POST operations must have a request body defined
  given: $.paths[*].post
  name: veryfi-post-requests-must-have-body
  severity: error
rules_file: rules/veryfi-ocr-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/veryfi/refs/heads/main/rules/veryfi-ocr-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: veryfi-ocr-rules
source_filename: veryfi-ocr-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  veryfi-operation-ids-camel-case:\n    description: Operation IDs must use camelCase as per Veryfi API conventions\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  veryfi-paths-must-use-partner-prefix:\n    description: All paths must be under /partner/ namespace\n    message: \"Path '{{path}}' must be under /partner/ namespace\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/partner/\"\n\n  veryfi-require-client-id-security:\n    description: All operations must declare clientId security\n    message: \"Operation must require CLIENT-ID authentication\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n\n  veryfi-document-responses-must-be-201:\n    description: Document creation endpoints must return 201 Created\n    message: \"POST document operations must return 201 Created\"\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '201'\n\n  veryfi-require-operation-description:\n    description: All operations must have a description\n    message: \"Operation must include a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  veryfi-require-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"\
  $.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  veryfi-error-responses-must-reference-schema:\n    description: Error responses must include a schema\n    message: \"Error responses must include a content schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses['4*','5*'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  veryfi-require-api-contact:\n    description: API info must include contact information\n    message: \"API info should include contact information\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  veryfi-document-id-must-be-integer:\n    description: Document IDs in paths must be integers\n    message: \"Document ID path parameters must be of type integer\"\n    severity: warn\n    given: \"$.paths[*][get,delete].parameters[?(@.name == 'documentId')].schema\"\
  \n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  veryfi-post-requests-must-have-body:\n    description: POST operations must have a request body defined\n    message: \"POST operation must define a requestBody\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/veryfi/refs/heads/main/rules/veryfi-ocr-rules.yml
tags:
- AI
- Document Processing
- Finance
- Invoices
- OCR
- Receipts
- Tax Forms
- Spectral
- Linting
- API Governance
---
