---
api_specs:
- filename: walt-disney-disney-api-openapi.yml
  format: yaml
  label: Disney Characters API
  slug: disney-characters-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walt-disney/refs/heads/main/openapi/walt-disney-disney-api-openapi.yml
categories:
- disney
description: Spectral linting rules defining API design standards and conventions for Walt Disney.
layout: rules
name: Walt Disney API Rules
provider_name: Walt Disney
provider_slug: walt-disney
rule_count: 9
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: disney-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: disney-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: disney-operation-tags-required
  severity: error
- description: List endpoints should support page and pageSize parameters
  given: $.paths[*].get.parameters
  name: disney-pagination-parameters
  severity: warn
- description: Info object must have a description
  given: $.info
  name: disney-info-description
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: disney-response-200-defined
  severity: error
- description: Successful responses should reference a schema
  given: $.paths[*][*].responses['200'].content['application/json']
  name: disney-response-schema-reference
  severity: warn
- description: Schemas should be defined in components for reuse
  given: $.components
  name: disney-schemas-in-components
  severity: warn
- description: At least one server must be defined
  given: $
  name: disney-server-defined
  severity: error
rules_file: rules/walt-disney-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/walt-disney/refs/heads/main/rules/walt-disney-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: walt-disney-rules
source_filename: walt-disney-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  disney-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  disney-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  disney-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  disney-pagination-parameters:\n    description: List endpoints should support page and pageSize parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\
  \          contains:\n            type: object\n            properties:\n              name:\n                enum:\n                  - page\n                  - pageSize\n\n  disney-info-description:\n    description: Info object must have a description\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  disney-response-200-defined:\n    description: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  disney-response-schema-reference:\n    description: Successful responses should reference a schema\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  disney-schemas-in-components:\n    description: Schemas should be defined in components for reuse\n    severity: warn\n    given: \"$.components\"\n    then:\n      field:\
  \ schemas\n      function: truthy\n\n  disney-server-defined:\n    description: At least one server must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/walt-disney/refs/heads/main/rules/walt-disney-rules.yml
tags:
- Entertainment
- Media
- Streaming
- Parks
- Content
- Spectral
- Linting
- API Governance
---
