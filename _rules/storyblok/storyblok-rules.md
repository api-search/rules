---
api_specs:
- filename: storyblok-content-delivery-api-v2-openapi.yml
  format: yaml
  label: Storyblok Content Delivery API
  slug: storyblok-content-delivery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-content-delivery-api-v2-openapi.yml
- filename: storyblok-management-api-openapi.yml
  format: yaml
  label: Storyblok Management API
  slug: storyblok-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-management-api-openapi.yml
- filename: storyblok-image-service-openapi.yml
  format: yaml
  label: Storyblok Image Service
  slug: storyblok-image-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-image-service-openapi.yml
- filename: storyblok-webhooks-asyncapi.yml
  format: yaml
  label: Storyblok Webhooks
  slug: storyblok-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/asyncapi/storyblok-webhooks-asyncapi.yml
categories:
- storyblok
description: Spectral linting rules defining API design standards and conventions for Storyblok.
layout: rules
name: Storyblok API Rules
provider_name: Storyblok
provider_slug: storyblok
rule_count: 10
rules:
- description: Management API endpoints must include space_id as a path parameter
  given: $.paths[?(@property.match(/\/spaces\//))].*.parameters[?(@.in == 'path')]
  name: storyblok-space-id-path-param
  severity: warn
- description: All server URLs must use HTTPS
  given: $.servers[*]
  name: storyblok-https-only
  severity: error
- description: All operations must have an operationId
  given: $.paths.*.*
  name: storyblok-operation-ids
  severity: error
- description: All operations must have a summary
  given: $.paths.*.*
  name: storyblok-operation-summary
  severity: warn
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: storyblok-tags-required
  severity: warn
- description: All operations should define a 401 Unauthorized response
  given: $.paths.*.*.responses
  name: storyblok-401-response
  severity: warn
- description: POST and PUT operations must accept application/json content type
  given: $.paths.*[post,put].requestBody.content
  name: storyblok-json-content-type
  severity: warn
- description: List operations should support pagination parameters
  given: $.paths[?(@property.match(/stories$|components$|assets$|datasources$|collaborators$/))].get.parameters[*]
  name: storyblok-pagination-params
  severity: info
- description: All parameters must have descriptions
  given: $.paths.*.*.parameters[*]
  name: storyblok-description-required
  severity: warn
- description: Server URLs should include API version
  given: $.servers[*]
  name: storyblok-version-in-server
  severity: info
rules_file: rules/storyblok-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/rules/storyblok-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 6
slug: storyblok-rules
source_filename: storyblok-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  storyblok-space-id-path-param:\n    description: Management API endpoints must include space_id as a path parameter\n    message: \"Management API path '{{path}}' should include {space_id} parameter\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/\\\\/spaces\\\\//))].*.parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: defined\n\n  storyblok-https-only:\n    description: All server URLs must use HTTPS\n    message: \"Server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  storyblok-operation-ids:\n    description: All operations must have an operationId\n    message: \"Operation at '{{path}}' must have an operationId\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: truthy\n\n  storyblok-operation-summary:\n    description:\
  \ All operations must have a summary\n    message: \"Operation at '{{path}}' must have a summary\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: summary\n      function: truthy\n\n  storyblok-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  storyblok-401-response:\n    description: All operations should define a 401 Unauthorized response\n    message: \"Operation should define a 401 response for unauthorized access\"\n    severity: warn\n    given: \"$.paths.*.*.responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  storyblok-json-content-type:\n    description: POST and PUT operations must accept application/json content type\n    message: \"POST/PUT operation should\
  \ accept application/json\"\n    severity: warn\n    given: \"$.paths.*[post,put].requestBody.content\"\n    then:\n      field: \"application/json\"\n      function: defined\n\n  storyblok-pagination-params:\n    description: List operations should support pagination parameters\n    message: \"List operation should include 'page' and 'per_page' parameters\"\n    severity: info\n    given: \"$.paths[?(@property.match(/stories$|components$|assets$|datasources$|collaborators$/))].get.parameters[*]\"\n    then:\n      field: name\n      function: defined\n\n  storyblok-description-required:\n    description: All parameters must have descriptions\n    message: \"Parameter '{{property}}' must have a description\"\n    severity: warn\n    given: \"$.paths.*.*.parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  storyblok-version-in-server:\n    description: Server URLs should include API version\n    message: \"Server URL should include version path component\"\n\
  \    severity: info\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/rules/storyblok-rules.yml
tags:
- CMS
- Content Delivery
- Content Management
- Headless CMS
- Image Optimization
- REST API
- Visual Editor
- Webhooks
- Spectral
- Linting
- API Governance
---
