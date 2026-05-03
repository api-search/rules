---
api_specs:
- filename: tripetto-form-builder-openapi.yml
  format: yaml
  label: Tripetto FormBuilder SDK
  slug: tripetto-form-builder-sdk
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tripetto/refs/heads/main/openapi/tripetto-form-builder-openapi.yml
categories:
- tripetto
description: Spectral linting rules defining API design standards and conventions for Tripetto.
layout: rules
name: Tripetto API Rules
provider_name: Tripetto
provider_slug: tripetto
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tripetto-operation-id-format
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: tripetto-require-tags
  severity: warn
- description: 200 responses must have a content body
  given: $.paths[*][*].responses['200']
  name: tripetto-response-200-has-content
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: tripetto-require-description
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: tripetto-path-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: tripetto-no-trailing-slash
  severity: error
- description: API must define Bearer authentication scheme
  given: $.components.securitySchemes
  name: tripetto-bearer-auth-defined
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: tripetto-schema-properties-have-description
  severity: info
rules_file: rules/tripetto-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tripetto/refs/heads/main/rules/tripetto-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: tripetto-rules
source_filename: tripetto-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Tripetto API Convention Rules\n\n  tripetto-operation-id-format:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase (e.g. listForms, createForm)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  tripetto-require-tags:\n    description: All operations must have at least one tag\n    message: Operations must be tagged for grouping (Forms, Responses, Webhooks)\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tripetto-response-200-has-content:\n    description: 200 responses must have a content body\n    message: Successful responses should return content\n    severity: warn\n    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: content\n      function: truthy\n\n  tripetto-require-description:\n\
  \    description: All operations must have a description\n    message: Operations must have a description explaining their purpose\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  tripetto-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{value}}' must use kebab-case for all segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  tripetto-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: \"Path '{{value}}' must not end with a trailing slash\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  tripetto-bearer-auth-defined:\n    description: API must define Bearer authentication scheme\n    message: Security scheme BearerAuth must be defined in components\n\
  \    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  tripetto-schema-properties-have-description:\n    description: Schema properties should have descriptions\n    message: \"Property '{{path}}' is missing a description\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tripetto/refs/heads/main/rules/tripetto-rules.yml
tags:
- Forms
- Surveys
- Form Builder
- No-Code
- SDK
- Webhooks
- Spectral
- Linting
- API Governance
---
