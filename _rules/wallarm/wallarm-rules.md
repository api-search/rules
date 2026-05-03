---
api_specs:
- filename: wallarm-openapi.yml
  format: yaml
  label: Wallarm API
  slug: wallarm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wallarm/refs/heads/main/openapi/wallarm-openapi.yml
categories:
- wallarm
description: Spectral linting rules defining API design standards and conventions for Wallarm.
layout: rules
name: Wallarm API Rules
provider_name: Wallarm
provider_slug: wallarm
rule_count: 12
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: wallarm-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: wallarm-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: wallarm-operation-tags-required
  severity: error
- description: Operations must use the Wallarm API token security scheme
  given: $.components.securitySchemes
  name: wallarm-security-scheme-apikey
  severity: error
- description: Operations must define at least a 200 and 401 response
  given: $.paths[*][*].responses
  name: wallarm-responses-defined
  severity: warn
- description: POST/PUT request bodies must specify application/json content type
  given: $.paths[*][post,put].requestBody.content
  name: wallarm-request-body-content-type
  severity: error
- description: v4 list endpoints should support pagination parameters
  given: $.paths['/v4/ip_rules'].get.parameters
  name: wallarm-v4-endpoints-paginated
  severity: warn
- description: Info object must have contact information
  given: $.info
  name: wallarm-info-contact
  severity: warn
- description: Info object must have a description
  given: $.info
  name: wallarm-info-description
  severity: error
- description: Both US and EU cloud servers must be defined
  given: $.servers
  name: wallarm-servers-defined
  severity: warn
- description: Components must define reusable schemas
  given: $.components
  name: wallarm-schemas-defined
  severity: warn
- description: Successful responses should reference a schema
  given: $.paths[*][*].responses['200'].content['application/json']
  name: wallarm-response-schema-reference
  severity: warn
rules_file: rules/wallarm-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wallarm/refs/heads/main/rules/wallarm-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 7
slug: wallarm-rules
source_filename: wallarm-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  wallarm-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wallarm-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  wallarm-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  wallarm-security-scheme-apikey:\n    description: Operations must use the Wallarm API token security scheme\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: ApiTokenAuth\n      function: truthy\n\n  wallarm-responses-defined:\n\
  \    description: Operations must define at least a 200 and 401 response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"200\"\n\n  wallarm-request-body-content-type:\n    description: POST/PUT request bodies must specify application/json content type\n    severity: error\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  wallarm-v4-endpoints-paginated:\n    description: v4 list endpoints should support pagination parameters\n    severity: warn\n    given: \"$.paths['/v4/ip_rules'].get.parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                enum:\n                  - limit\n                  - offset\n\
  \n  wallarm-info-contact:\n    description: Info object must have contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  wallarm-info-description:\n    description: Info object must have a description\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  wallarm-servers-defined:\n    description: Both US and EU cloud servers must be defined\n    severity: warn\n    given: \"$.servers\"\n    then:\n      function: length\n      functionOptions:\n        min: 2\n\n  wallarm-schemas-defined:\n    description: Components must define reusable schemas\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n\n  wallarm-response-schema-reference:\n    description: Successful responses should reference a schema\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json']\"\n    then:\n   \
  \   field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wallarm/refs/heads/main/rules/wallarm-rules.yml
tags:
- API Security
- Security Testing
- WAF
- Cybersecurity
- Spectral
- Linting
- API Governance
---
