---
api_specs:
- filename: whisky-hunter-openapi.yml
  format: yaml
  label: Whisky Hunter API
  slug: whisky-hunter
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/whisky-hunter/refs/heads/main/openapi/whisky-hunter-openapi.yml
categories:
- whisky
description: Spectral linting rules defining API design standards and conventions for Whisky Hunter.
layout: rules
name: Whisky Hunter API Rules
provider_name: Whisky Hunter
provider_slug: whisky-hunter
rule_count: 9
rules:
- description: The Whisky Hunter API is public and should not declare security requirements.
  given: $.paths.*.*
  name: whisky-hunter-no-auth-required
  severity: warn
- description: Whisky Hunter API paths end with a trailing slash per convention.
  given: $.paths.*~
  name: whisky-hunter-trailing-slash-paths
  severity: warn
- description: GET endpoints should support the format query parameter for JSON output.
  given: $.paths.*.get
  name: whisky-hunter-format-query-param
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths.*.get
  name: whisky-hunter-response-200-defined
  severity: error
- description: Data endpoints should return arrays.
  given: $.paths.*.get.responses.200.content.application/json.schema
  name: whisky-hunter-array-response-for-data-endpoints
  severity: warn
- description: All operationIds should use camelCase.
  given: $.paths.*.*.operationId
  name: whisky-hunter-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths.*.*
  name: whisky-hunter-tags-on-operations
  severity: error
- description: All operations should have a description.
  given: $.paths.*.*
  name: whisky-hunter-description-on-operations
  severity: warn
- description: Distillery data path must use {slug} path parameter.
  given: $.paths[?(@property.includes('distillery_data'))].get.parameters[*]
  name: whisky-hunter-slug-path-param
  severity: warn
rules_file: rules/whisky-hunter-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/whisky-hunter/refs/heads/main/rules/whisky-hunter-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 7
slug: whisky-hunter-rules
source_filename: whisky-hunter-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  whisky-hunter-no-auth-required:\n    description: The Whisky Hunter API is public and should not declare security requirements.\n    message: Whisky Hunter API operations should not require authentication.\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: security\n      function: falsy\n\n  whisky-hunter-trailing-slash-paths:\n    description: Whisky Hunter API paths end with a trailing slash per convention.\n    message: Path '{{path}}' should end with a trailing slash per Whisky Hunter convention.\n    severity: warn\n    given: \"$.paths.*~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/$\"\n\n  whisky-hunter-format-query-param:\n    description: GET endpoints should support the format query parameter for JSON output.\n    message: GET operation at '{{path}}' should document the format query parameter.\n    severity: warn\n    given: \"$.paths.*.get\"\n    then:\n      field: parameters\n\
  \      function: truthy\n\n  whisky-hunter-response-200-defined:\n    description: All GET operations must define a 200 response.\n    message: GET operation at '{{path}}' must define a 200 response.\n    severity: error\n    given: \"$.paths.*.get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  whisky-hunter-array-response-for-data-endpoints:\n    description: Data endpoints should return arrays.\n    message: Data endpoint '{{path}}' should return an array in the 200 response schema.\n    severity: warn\n    given: \"$.paths.*.get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              enum:\n                - array\n\n  whisky-hunter-operation-ids-camel-case:\n    description: All operationIds should use camelCase.\n    message: OperationId '{{value}}' should use camelCase.\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n   \
  \ then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  whisky-hunter-tags-on-operations:\n    description: All operations must have at least one tag.\n    message: Operation '{{path}}' must have at least one tag.\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  whisky-hunter-description-on-operations:\n    description: All operations should have a description.\n    message: Operation '{{path}}' is missing a description.\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: description\n      function: truthy\n\n  whisky-hunter-slug-path-param:\n    description: Distillery data path must use {slug} path parameter.\n    message: Distillery data path should use {slug} path parameter.\n    severity: warn\n    given: \"$.paths[?(@property.includes('distillery_data'))].get.parameters[*]\"\n    then:\n      field: name\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/whisky-hunter/refs/heads/main/rules/whisky-hunter-rules.yml
tags:
- Whisky
- Spirits
- Auctions
- Market Data
- Collectors
- Investors
- Spectral
- Linting
- API Governance
---
