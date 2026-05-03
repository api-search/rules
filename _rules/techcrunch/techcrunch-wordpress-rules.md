---
api_specs:
- filename: techcrunch-wordpress-rest-api-openapi.yml
  format: yaml
  label: TechCrunch WordPress REST API
  slug: wordpress-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/techcrunch/refs/heads/main/openapi/techcrunch-wordpress-rest-api-openapi.yml
categories:
- wp
description: Spectral linting rules defining API design standards and conventions for TechCrunch.
layout: rules
name: TechCrunch API Rules
provider_name: TechCrunch
provider_slug: techcrunch
rule_count: 12
rules:
- description: All operations must have an operationId
  given: $.paths.*.*
  name: wp-operationid-required
  severity: error
- description: Operation IDs must use camelCase (WordPress REST API convention)
  given: $.paths.*.*.operationId
  name: wp-operationid-camel-case
  severity: warn
- description: List endpoints should support page and per_page query parameters
  given: $.paths[?(!@property.match(/\/\{id\}$/))].get
  name: wp-get-operations-support-pagination
  severity: warn
- description: per_page parameter should enforce a maximum of 100
  given: $.paths.*.get.parameters[?(@.name == 'per_page')].schema
  name: wp-per-page-max-100
  severity: warn
- description: The {id} path parameter must be an integer
  given: $.paths[?(@property =~ /\{id\}/)].*.parameters[?(@.name == 'id')].schema
  name: wp-id-path-param-integer
  severity: error
- description: All GET operations must have a 200 response defined
  given: $.paths.*.get
  name: wp-response-200-required
  severity: error
- description: 4xx responses should use WPError schema
  given: $.paths.*.*.responses[?(@property >= '400' && @property < '500')]
  name: wp-error-schema-on-4xx
  severity: warn
- description: All operations must be tagged for grouping
  given: $.paths.*.*
  name: wp-tags-on-operations
  severity: error
- description: All operations must have a description
  given: $.paths.*.*
  name: wp-description-on-operations
  severity: warn
- description: TechCrunch WordPress REST API is read-only public - no auth required
  given: $.paths.*.get
  name: wp-no-auth-required
  severity: info
- description: The /search endpoint must have a required search parameter
  given: $.paths['/search'].get.parameters[?(@.name == 'search')]
  name: wp-search-requires-search-param
  severity: error
- description: Post/page content should use RenderedValue schema pattern
  given: $.components.schemas.Post.properties[?(@property =~ /^(title|content|excerpt|guid)$/)]
  name: wp-rendered-content-schema
  severity: info
rules_file: rules/techcrunch-wordpress-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/techcrunch/refs/heads/main/rules/techcrunch-wordpress-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 5
slug: techcrunch-wordpress-rules
source_filename: techcrunch-wordpress-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # WordPress REST API conventions\n  wp-operationid-required:\n    description: All operations must have an operationId\n    message: \"Missing operationId: {{path}}\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: truthy\n\n  wp-operationid-camel-case:\n    description: Operation IDs must use camelCase (WordPress REST API convention)\n    message: \"Operation ID '{{value}}' must be camelCase: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  wp-get-operations-support-pagination:\n    description: List endpoints should support page and per_page query parameters\n    message: \"List operation should support pagination parameters: {{path}}\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/\\\\/\\\\{id\\\\}$/))].get\"\n    then:\n      field: parameters\n\
  \      function: truthy\n\n  wp-per-page-max-100:\n    description: per_page parameter should enforce a maximum of 100\n    message: \"per_page parameter must have maximum: 100: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.get.parameters[?(@.name == 'per_page')].schema\"\n    then:\n      field: maximum\n      function: defined\n\n  wp-id-path-param-integer:\n    description: The {id} path parameter must be an integer\n    message: \"Path parameter 'id' must be type integer: {{path}}\"\n    severity: error\n    given: \"$.paths[?(@property =~ /\\\\{id\\\\}/)].*.parameters[?(@.name == 'id')].schema\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  wp-response-200-required:\n    description: All GET operations must have a 200 response defined\n    message: \"GET operation missing 200 response: {{path}}\"\n    severity: error\n    given: \"$.paths.*.get\"\n    then:\n      field: responses.200\n      function:\
  \ truthy\n\n  wp-error-schema-on-4xx:\n    description: 4xx responses should use WPError schema\n    message: \"4xx response should define error schema: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*.responses[?(@property >= '400' && @property < '500')]\"\n    then:\n      field: content\n      function: truthy\n\n  wp-tags-on-operations:\n    description: All operations must be tagged for grouping\n    message: \"Operation missing tags: {{path}}\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  wp-description-on-operations:\n    description: All operations must have a description\n    message: \"Operation missing description: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: description\n      function: truthy\n\n  wp-no-auth-required:\n    description: TechCrunch WordPress REST API is read-only public - no auth required\n    message: \"Public read operations should not require authentication:\
  \ {{path}}\"\n    severity: info\n    given: \"$.paths.*.get\"\n    then:\n      field: security\n      function: falsy\n\n  wp-search-requires-search-param:\n    description: The /search endpoint must have a required search parameter\n    message: \"Search endpoint must have required search parameter: {{path}}\"\n    severity: error\n    given: \"$.paths['/search'].get.parameters[?(@.name == 'search')]\"\n    then:\n      field: required\n      function: truthy\n\n  wp-rendered-content-schema:\n    description: Post/page content should use RenderedValue schema pattern\n    message: \"Content fields should use RenderedValue schema: {{path}}\"\n    severity: info\n    given: \"$.components.schemas.Post.properties[?(@property =~ /^(title|content|excerpt|guid)$/)]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/techcrunch/refs/heads/main/rules/techcrunch-wordpress-rules.yml
tags:
- Media
- News
- Startups
- Technology News
- Venture Capital
- Spectral
- Linting
- API Governance
---
