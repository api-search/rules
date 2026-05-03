---
api_specs:
- filename: volkswagen-okapi-openapi.yml
  format: yaml
  label: Volkswagen OKAPI - Open Konfigurator API
  slug: volkswagen-okapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/volkswagen/refs/heads/main/openapi/volkswagen-okapi-openapi.yml
categories:
- volkswagen
description: Spectral linting rules defining API design standards and conventions for Volkswagen.
layout: rules
name: Volkswagen API Rules
provider_name: Volkswagen
provider_slug: volkswagen
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: volkswagen-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: volkswagen-operation-ids-camel-case
  severity: warn
- description: Each operation must have at least one tag.
  given: $.paths[*][*]
  name: volkswagen-tags-required
  severity: error
- description: API must declare Bearer authentication.
  given: $.components.securitySchemes
  name: volkswagen-bearer-auth-required
  severity: error
- description: Operation paths should include a countryCode path parameter.
  given: $.paths[*operation*][post,get].parameters[*]
  name: volkswagen-country-code-path-param
  severity: info
- description: Server URL must include an API version prefix.
  given: $.servers[*].url
  name: volkswagen-version-in-server-url
  severity: warn
- description: Catalog endpoints should use GET method.
  given: $.paths[*/catalog/*]
  name: volkswagen-catalog-endpoints-get
  severity: warn
- description: Operation endpoints (buildability, config, information) should use POST method.
  given: $.paths[*/operation/*]
  name: volkswagen-operation-endpoints-post
  severity: warn
rules_file: rules/volkswagen-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/volkswagen/refs/heads/main/rules/volkswagen-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: volkswagen-rules
source_filename: volkswagen-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  volkswagen-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*(\\\\s[A-Z][a-z]*)*)\"\n\n  volkswagen-operation-ids-camel-case:\n    description: OperationIds must use camelCase.\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  volkswagen-tags-required:\n    description: Each operation must have at least one tag.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  volkswagen-bearer-auth-required:\n    description: API must declare Bearer authentication.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  volkswagen-country-code-path-param:\n\
  \    description: Operation paths should include a countryCode path parameter.\n    severity: info\n    given: \"$.paths[*operation*][post,get].parameters[*]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - countryCode\n          - brandId\n          - modelId\n          - typeId\n\n  volkswagen-version-in-server-url:\n    description: Server URL must include an API version prefix.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\/v[0-9]+.*\"\n\n  volkswagen-catalog-endpoints-get:\n    description: Catalog endpoints should use GET method.\n    severity: warn\n    given: \"$.paths[*/catalog/*]\"\n    then:\n      field: get\n      function: truthy\n\n  volkswagen-operation-endpoints-post:\n    description: Operation endpoints (buildability, config, information) should use POST method.\n    severity: warn\n    given: \"$.paths[*/operation/*]\"\
  \n    then:\n      field: post\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/volkswagen/refs/heads/main/rules/volkswagen-rules.yml
tags:
- Automobiles
- Cars
- Vehicles
- Automotive
- Vehicle Configuration
- Spectral
- Linting
- API Governance
---
