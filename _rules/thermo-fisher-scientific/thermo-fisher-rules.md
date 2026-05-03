---
api_specs:
- filename: thermo-fisher-samplemanager-openapi.yml
  format: yaml
  label: Thermo Fisher SampleManager LIMS REST API
  slug: samplemanager-lims
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thermo-fisher-scientific/refs/heads/main/openapi/thermo-fisher-samplemanager-openapi.yml
- filename: thermo-fisher-nanodrop-openapi.yml
  format: yaml
  label: Thermo Fisher NanoDrop Ultra Web API
  slug: nanodrop-ultra
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thermo-fisher-scientific/refs/heads/main/openapi/thermo-fisher-nanodrop-openapi.yml
categories:
- thermo
description: Spectral linting rules defining API design standards and conventions for Thermo Fisher Scientific.
layout: rules
name: Thermo Fisher Scientific API Rules
provider_name: Thermo Fisher Scientific
provider_slug: thermo-fisher-scientific
rule_count: 9
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thermo-fisher-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: thermo-fisher-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: thermo-fisher-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: thermo-fisher-description-required
  severity: warn
- description: Non-public operations must declare authentication.
  given: $.paths[*][get,post,put,patch,delete]
  name: thermo-fisher-auth-defined
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths[*][get].responses
  name: thermo-fisher-200-response-defined
  severity: error
- description: All authenticated operations must define a 401 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: thermo-fisher-401-response-defined
  severity: warn
- description: All path segments must use kebab-case or camelCase (matching LIMS patterns).
  given: $.paths[*]~
  name: thermo-fisher-path-kebab-case
  severity: info
- description: POST operations should define a request body.
  given: $.paths[*][post]
  name: thermo-fisher-request-body-post
  severity: warn
rules_file: rules/thermo-fisher-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thermo-fisher-scientific/refs/heads/main/rules/thermo-fisher-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: thermo-fisher-rules
source_filename: thermo-fisher-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  thermo-fisher-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  thermo-fisher-operation-ids-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  thermo-fisher-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  thermo-fisher-description-required:\n\
  \    description: All operations must have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  thermo-fisher-auth-defined:\n    description: Non-public operations must declare authentication.\n    message: \"Operation at '{{path}}' should declare security scheme.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  thermo-fisher-200-response-defined:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  thermo-fisher-401-response-defined:\n    description: All authenticated operations\
  \ must define a 401 response.\n    message: \"Authenticated operation at '{{path}}' should define a 401 response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  thermo-fisher-path-kebab-case:\n    description: All path segments must use kebab-case or camelCase (matching LIMS patterns).\n    message: \"Path '{{path}}' segments should use lowercase.\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9{}_-]*)*$\"\n\n  thermo-fisher-request-body-post:\n    description: POST operations should define a request body.\n    message: \"POST operation at '{{path}}' should define a request body.\"\n    severity: warn\n    given: \"$.paths[*][post]\"\n    then:\n      field: requestBody\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thermo-fisher-scientific/refs/heads/main/rules/thermo-fisher-rules.yml
tags:
- Life Sciences
- Laboratory
- Scientific Instruments
- LIMS
- Diagnostics
- Biosciences
- Fortune 500
- Spectral
- Linting
- API Governance
---
