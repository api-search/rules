---
api_specs:
- filename: sanity-openapi.yml
  format: yaml
  label: Sanity Query API
  slug: sanity-query-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sanity/refs/heads/main/openapi/sanity-openapi.yml
categories:
- sanity
description: Spectral linting rules defining API design standards and conventions for Sanity.
layout: rules
name: Sanity API Rules
provider_name: Sanity
provider_slug: sanity
rule_count: 7
rules:
- description: All Sanity API endpoints must use Bearer token authentication
  given: $.paths[*][*]
  name: sanity-bearer-auth-required
  severity: error
- description: Sanity API servers must use HTTPS
  given: $.servers[*]
  name: sanity-https-servers-only
  severity: error
- description: All operations must define operationId for client code generation
  given: $.paths[*][*]
  name: sanity-operation-id-required
  severity: error
- description: All operations must have tags for grouping
  given: $.paths[*][*]
  name: sanity-tags-required
  severity: warn
- description: Data operations should include dataset as path parameter
  given: $.paths['/data/*'][*]
  name: sanity-dataset-path-parameter
  severity: warn
- description: All Sanity operations should define a 200 or 201 response
  given: $.paths[*][*].responses
  name: sanity-response-200-defined
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: sanity-description-required
  severity: warn
rules_file: rules/sanity-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sanity/refs/heads/main/rules/sanity-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: sanity-rules
source_filename: sanity-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sanity-bearer-auth-required:\n    description: All Sanity API endpoints must use Bearer token authentication\n    message: \"Endpoint {{path}} must use BearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n\n  sanity-https-servers-only:\n    description: Sanity API servers must use HTTPS\n    message: \"Server URL must begin with https://\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  sanity-operation-id-required:\n    description: All operations must define operationId for client code generation\n    message: \"Operation at {{path}} must have operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function:\
  \ truthy\n\n  sanity-tags-required:\n    description: All operations must have tags for grouping\n    message: \"Operation {{operationId}} must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  sanity-dataset-path-parameter:\n    description: Data operations should include dataset as path parameter\n    message: \"Data operation paths should include {dataset} path parameter\"\n    severity: warn\n    given: \"$.paths['/data/*'][*]\"\n    then:\n      field: parameters\n      function: truthy\n\n  sanity-response-200-defined:\n    description: All Sanity operations should define a 200 or 201 response\n    message: \"Operation {{path}} should define a success response\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"\
  201\"]\n\n  sanity-description-required:\n    description: All operations must have a description\n    message: \"Operation {{operationId}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sanity/refs/heads/main/rules/sanity-rules.yml
tags:
- Headless CMS
- Content Management
- GROQ
- Real-Time
- Structured Content
- Developer Platform
- Spectral
- Linting
- API Governance
---
