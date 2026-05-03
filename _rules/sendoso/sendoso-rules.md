---
api_specs:
- filename: sendoso-api-openapi.yml
  format: yaml
  label: Sendoso Sending Platform API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sendoso/main/openapi/sendoso-api-openapi.yml
categories:
- sendoso
description: Spectral linting rules defining API design standards and conventions for Sendoso.
layout: rules
name: Sendoso API Rules
provider_name: Sendoso
provider_slug: sendoso
rule_count: 8
rules:
- description: Sendoso operationIds use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sendoso-operation-id-camel-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sendoso-operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sendoso-operation-summary-required
  severity: error
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: sendoso-operation-tags-required
  severity: error
- description: Operations must use defined tags
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: sendoso-valid-tags
  severity: warn
- description: List operations should support page and per_page pagination
  given: $.paths[*].get
  name: sendoso-list-pagination
  severity: info
- description: API must define security (X-Api-Key)
  given: $
  name: sendoso-security-defined
  severity: error
- description: Operations must define success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sendoso-success-response
  severity: error
rules_file: rules/sendoso-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sendoso/refs/heads/main/rules/sendoso-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 2
slug: sendoso-rules
source_filename: sendoso-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Sendoso uses snake_case for all field names\n  sendoso-operation-id-camel-case:\n    description: Sendoso operationIds use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations require operationId\n  sendoso-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # All operations must have a summary\n  sendoso-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: summary\n      function: defined\n\n  # Operations must have tags\n  sendoso-operation-tags-required:\n    description: All operations must be tagged\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  # Tags must be from the defined list\n  sendoso-valid-tags:\n    description: Operations must use defined tags\n    message: \"Tag '{{value}}' is not in the Sendoso tag list\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Sends\n          - Recipients\n          - Teams\n          - Inventory\n          - Reports\n\n  # Pagination: list endpoints must have page and per_page\n  sendoso-list-pagination:\n    description: List operations should support page and per_page\
  \ pagination\n    message: \"GET list operations should include pagination parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: defined\n\n  # Security must be defined globally\n  sendoso-security-defined:\n    description: API must define security (X-Api-Key)\n    message: \"Global security must be defined\"\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: defined\n\n  # Responses must include 200 or 201\n  sendoso-success-response:\n    description: Operations must define success response\n    message: \"Operation must define a 200 or 201 response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sendoso/refs/heads/main/rules/sendoso-rules.yml
tags:
- Corporate Gifting
- Direct Mail
- Sales Engagement
- Marketing Automation
- CRM Integration
- Spectral
- Linting
- API Governance
---
