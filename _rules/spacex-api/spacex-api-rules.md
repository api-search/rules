---
api_specs:
- filename: spacex-api-openapi.yml
  format: yaml
  label: SpaceX API
  slug: spacex-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spacex-api/refs/heads/main/openapi/spacex-api-openapi.yml
categories:
- spacex
description: Spectral linting rules defining API design standards and conventions for SpaceX API.
layout: rules
name: SpaceX API API Rules
provider_name: SpaceX API
provider_slug: spacex-api
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spacex-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: spacex-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spacex-tags-title-case
  severity: warn
- description: Resource collections should expose both list and get-by-id operations
  given: $.paths[*]
  name: spacex-resource-has-list-and-get
  severity: info
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: spacex-response-must-have-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: spacex-schema-properties-have-descriptions
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: spacex-servers-must-be-https
  severity: error
- description: SpaceX API path parameters for entity lookup should be named id
  given: $.paths[*].get.parameters[?(@.in=='path')]
  name: spacex-path-parameters-must-be-id
  severity: info
rules_file: rules/spacex-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spacex-api/refs/heads/main/rules/spacex-api-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 4
slug: spacex-api-rules
source_filename: spacex-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  spacex-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9-]*)(\\\\s[A-Z][a-z0-9-]*)*$\"\n\n  spacex-operation-id-camel-case:\n    description: All operationIds must use camelCase\n    message: OperationId \"{{value}}\" must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spacex-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9-]*)(\\\\s[A-Z][a-z0-9-]*)*$\"\n\n  spacex-resource-has-list-and-get:\n\
  \    description: Resource collections should expose both list and get-by-id operations\n    message: Path must have corresponding GET operations for collection and single item\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      field: get\n      function: truthy\n\n  spacex-response-must-have-description:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spacex-schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    message: Schema property \"{{path}}\" should have a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spacex-servers-must-be-https:\n    description: All server URLs must use HTTPS\n    message: Server URL \"{{value}}\" must use HTTPS\n\
  \    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  spacex-path-parameters-must-be-id:\n    description: SpaceX API path parameters for entity lookup should be named id\n    message: Path parameter for resource lookup should be named id\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.in=='path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - id\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spacex-api/refs/heads/main/rules/spacex-api-rules.yml
tags:
- Space
- Aerospace
- Launches
- SpaceX
- Spectral
- Linting
- API Governance
---
