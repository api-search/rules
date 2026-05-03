---
api_specs:
- filename: openapi.json
  format: json
  label: SpaceAPI Collector
  slug: spaceapi-collector
  spec_type: OpenAPI
  url: https://api.spaceapi.io/openapi.json
categories:
- spaceapi
description: Spectral linting rules defining API design standards and conventions for SpaceAPI.
layout: rules
name: SpaceAPI API Rules
provider_name: SpaceAPI
provider_slug: spaceapi
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spaceapi-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: spaceapi-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spaceapi-tags-title-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: spaceapi-operation-must-have-tags
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: spaceapi-response-must-have-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: spaceapi-schema-properties-have-descriptions
  severity: info
- description: API must have contact information
  given: $.info
  name: spaceapi-info-contact
  severity: warn
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: spaceapi-servers-must-be-https
  severity: error
rules_file: rules/spaceapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spaceapi/refs/heads/main/rules/spaceapi-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 6
slug: spaceapi-rules
source_filename: spaceapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  spaceapi-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*)(\\\\s[A-Z][a-z0-9]*)*$\"\n\n  spaceapi-operation-id-camel-case:\n    description: All operationIds must use camelCase\n    message: OperationId \"{{value}}\" must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spaceapi-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*)(\\\\s[A-Z][a-z0-9]*)*$\"\n\n  spaceapi-operation-must-have-tags:\n\
  \    description: Every operation must have at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  spaceapi-response-must-have-description:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spaceapi-schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    message: Schema property \"{{path}}\" should have a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spaceapi-info-contact:\n    description: API must have contact information\n    message: API info must include contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field:\
  \ contact\n      function: truthy\n\n  spaceapi-servers-must-be-https:\n    description: All server URLs must use HTTPS\n    message: Server URL \"{{value}}\" must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spaceapi/refs/heads/main/rules/spaceapi-rules.yml
tags:
- Co-Working
- Event Spaces
- Maker Spaces
- Hackerspaces
- Community
- Open Standard
- Spectral
- Linting
- API Governance
---
