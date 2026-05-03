---
api_specs:
- filename: texas-instruments-store-openapi.yml
  format: yaml
  label: Texas Instruments Store API
  slug: ti-store-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/texas-instruments/refs/heads/main/openapi/texas-instruments-store-openapi.yml
- filename: texas-instruments-product-information-openapi.yml
  format: yaml
  label: Texas Instruments Product Information API
  slug: ti-product-information-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/texas-instruments/refs/heads/main/openapi/texas-instruments-product-information-openapi.yml
categories:
- ti
description: Spectral linting rules defining API design standards and conventions for Texas Instruments.
layout: rules
name: Texas Instruments API Rules
provider_name: Texas Instruments
provider_slug: texas-instruments
rule_count: 7
rules:
- description: TI API paths should include version prefix
  given: $.paths[*]~
  name: ti-path-version-prefix
  severity: warn
- description: All TI API operations must use OAuth2 authentication
  given: $.paths[*][get,post,put,delete]
  name: ti-oauth2-security
  severity: error
- description: Part number path parameters should be named partNumber
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: ti-part-number-param-name
  severity: info
- description: Successful responses must return content
  given: $.paths[*][get,post].responses.200
  name: ti-200-response-content
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete]
  name: ti-operation-summary
  severity: error
- description: Tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: ti-tags-title-case
  severity: warn
- description: POST create operations should return HTTP 201
  given: $.paths[*].post
  name: ti-create-returns-201
  severity: info
rules_file: rules/texas-instruments-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/texas-instruments/refs/heads/main/rules/texas-instruments-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 3
slug: texas-instruments-rules
source_filename: texas-instruments-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # TI API: Paths must use versioned base paths\n  ti-path-version-prefix:\n    description: TI API paths should include version prefix\n    message: Path \"{{value}}\" should use a versioned path (e.g., /v1/ or /v2/)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  # TI API: OAuth2 must be defined for all operations\n  ti-oauth2-security:\n    description: All TI API operations must use OAuth2 authentication\n    message: Operation must define OAuth2 security\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [security]\n            - {}\n\n  # TI API: Part number path params must use specific name\n  ti-part-number-param-name:\n    description: Part number path parameters should be named partNumber\n    message: Part\
  \ number parameter should be named \"partNumber\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          not:\n            properties:\n              name:\n                enum: [part, part_number, partnumber, opn]\n\n  # TI API: 200 responses must have content\n  ti-200-response-content:\n    description: Successful responses must return content\n    message: Response 200 must include content definition\n    severity: warn\n    given: \"$.paths[*][get,post].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  # TI API: All operations must have summaries\n  ti-operation-summary:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # TI API: Tags must use Title Case\n  ti-tags-title-case:\n\
  \    description: Tags must use Title Case\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # TI API: POST create operations should return 201\n  ti-create-returns-201:\n    description: POST create operations should return HTTP 201\n    message: POST operation that creates resources should return 201\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            responses:\n              anyOf:\n                - required: [\"201\"]\n                - required: [\"200\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/texas-instruments/refs/heads/main/rules/texas-instruments-rules.yml
tags:
- Electronics
- Ordering
- Semiconductors
- Supply Chain
- Spectral
- Linting
- API Governance
---
