---
api_specs:
- filename: unum-hr-connect-openapi.yml
  format: yaml
  label: Unum HR Connect API
  slug: hr-connect
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unum/refs/heads/main/openapi/unum-hr-connect-openapi.yml
categories:
- unum
description: Spectral linting rules defining API design standards and conventions for Unum.
layout: rules
name: Unum API Rules
provider_name: Unum
provider_slug: unum
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: unum-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: unum-path-kebab-case
  severity: warn
- description: Collection endpoints should require groupId query parameter for multi-tenant isolation
  given: $.paths[?(!@property.match(/{.*}/))].get
  name: unum-require-group-id
  severity: warn
- description: List operations must support pagination parameters
  given: $.paths[*].get
  name: unum-require-pagination
  severity: warn
- description: Date fields should use ISO 8601 format
  given: $.components.schemas[*].properties[?(@.type == 'string')]
  name: unum-dates-iso8601
  severity: warn
- description: List responses should use a data envelope with pagination metadata
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: unum-response-envelope
  severity: warn
- description: Error responses must use consistent error schema with code and message
  given: $.paths[*][*].responses[?(@property >= '400')].content.application/json.schema
  name: unum-error-schema
  severity: warn
- description: All paths must declare OAuth2 security
  given: $.paths[*][get,post,put,delete]
  name: unum-oauth2-security
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: unum-operation-summaries-title-case
  severity: warn
- description: All operation tags must reference tags defined in the top-level tags array
  given: $.paths[*][*].tags[*]
  name: unum-tags-defined
  severity: warn
rules_file: rules/unum-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unum/refs/heads/main/rules/unum-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 10
slug: unum-rules
source_filename: unum-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Unum API naming conventions\n  unum-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  unum-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{path}}' must use kebab-case segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  unum-require-group-id:\n    description: Collection endpoints should require groupId query parameter for multi-tenant isolation\n    message: \"Collection endpoint '{{path}}' should require a groupId query parameter\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/{.*}/))].get\"\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            parameters:\n              type: array\n              contains:\n                type: object\n                properties:\n                  name:\n                    type: string\n                    enum: [groupId]\n                  required:\n                    type: boolean\n                    enum: [true]\n\n  unum-require-pagination:\n    description: List operations must support pagination parameters\n    message: \"List operation should include page and limit parameters\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            parameters:\n              type: array\n              contains:\n                type: object\n                properties:\n                  name:\n                    type: string\n                    enum: [page,\
  \ limit]\n\n  unum-dates-iso8601:\n    description: Date fields should use ISO 8601 format\n    message: \"Date field '{{path}}' should use format: date or date-time\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.type == 'string')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          if:\n            properties:\n              description:\n                type: string\n                pattern: \"[Dd]ate|[Tt]ime\"\n          then:\n            properties:\n              format:\n                type: string\n                enum: [date, date-time]\n\n  unum-response-envelope:\n    description: List responses should use a data envelope with pagination metadata\n    message: \"List response should include data array, total, page, and limit fields\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          properties:\n            properties:\n              type: object\n              required: [data]\n\n  unum-error-schema:\n    description: Error responses must use consistent error schema with code and message\n    message: \"Error response should reference the standard Error schema\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '400')].content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            $ref:\n              type: string\n\n  unum-oauth2-security:\n    description: All paths must declare OAuth2 security\n    message: \"Operation at '{{path}}' should declare OAuth2 security requirements\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required:\
  \ [security]\n            - properties:\n                operationId:\n                  type: string\n                  enum: [getAccessToken]\n\n  unum-operation-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]* ?)+$\"\n\n  unum-tags-defined:\n    description: All operation tags must reference tags defined in the top-level tags array\n    message: \"Operation uses undefined tag '{{value}}'\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Eligibility\n          - Enrollment\n          - Leave Management\n          - Evidence of Insurability\n          - Billing\n          - Authentication\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unum/refs/heads/main/rules/unum-rules.yml
tags:
- Insurance
- Benefits Administration
- HR Integration
- Disability Insurance
- Life Insurance
- Spectral
- Linting
- API Governance
---
