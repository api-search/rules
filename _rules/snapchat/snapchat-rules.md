---
api_specs:
- filename: snapchat-ads-api-openapi.yml
  format: yaml
  label: Snapchat Ads API
  slug: snapchat-ads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snapchat/refs/heads/main/openapi/snapchat-ads-api-openapi.yml
- filename: snapchat-conversions-api-openapi.yml
  format: yaml
  label: Snapchat Conversions API
  slug: snapchat-conversions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snapchat/refs/heads/main/openapi/snapchat-conversions-api-openapi.yml
- filename: snapchat-login-kit-openapi.yml
  format: yaml
  label: Snapchat Login Kit API
  slug: snapchat-login-kit
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snapchat/refs/heads/main/openapi/snapchat-login-kit-openapi.yml
categories:
- snapchat
description: Spectral linting rules defining API design standards and conventions for Snapchat.
layout: rules
name: Snapchat API Rules
provider_name: Snapchat
provider_slug: snapchat
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: snapchat-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case or path parameters
  given: $.paths[*]~
  name: snapchat-path-kebab-case
  severity: warn
- description: Snapchat Ads API responses use an envelope pattern with request_status and request_id fields in 200 responses.
  given: $.paths[*][get,post,put].responses['200'].content['application/json'].schema.properties
  name: snapchat-response-envelope
  severity: info
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,delete,patch]
  name: snapchat-security-defined
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: snapchat-operation-tag
  severity: warn
- description: All operations must have a summary in Title Case
  given: $.paths[*][get,post,put,delete,patch]
  name: snapchat-operation-summary
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: snapchat-operation-description
  severity: info
- description: Request and response bodies should use application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: snapchat-json-content-type
  severity: info
- description: Path parameters should use snake_case
  given: $.paths[*][*].parameters[*][?(@.in == 'path')].name
  name: snapchat-path-param-naming
  severity: info
- description: Servers should include a versioned base path (v1, v2, v3)
  given: $.servers[*].url
  name: snapchat-server-versioned
  severity: warn
rules_file: rules/snapchat-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/snapchat/refs/heads/main/rules/snapchat-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 4
  warn: 5
slug: snapchat-rules
source_filename: snapchat-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Naming conventions\n  snapchat-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: \"operationId '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  snapchat-path-kebab-case:\n    description: Path segments must use kebab-case or path parameters\n    message: \"Path segment must use kebab-case or path parameters: {{value}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z_]+\\\\})+/?$\"\n\n  # Response conventions\n  snapchat-response-envelope:\n    description: >-\n      Snapchat Ads API responses use an envelope pattern with request_status\n      and request_id fields in 200 responses.\n    message: \"200 responses should include request_status\
  \ and request_id envelope fields\"\n    severity: info\n    given: \"$.paths[*][get,post,put].responses['200'].content['application/json'].schema.properties\"\n    then:\n      function: truthy\n\n  # Auth requirements\n  snapchat-security-defined:\n    description: All operations must define security requirements\n    message: \"Operation must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: security\n      function: truthy\n\n  # Tag requirements\n  snapchat-operation-tag:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag for grouping\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summary requirements\n  snapchat-operation-summary:\n    description: All operations must have a summary in Title Case\n    message: \"Operation must have a summary\"\n    severity:\
  \ warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Description requirements\n  snapchat-operation-description:\n    description: All operations should have a description\n    message: \"Operation should have a detailed description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  # Media type conventions\n  snapchat-json-content-type:\n    description: Request and response bodies should use application/json\n    message: \"Content type should be application/json\"\n    severity: info\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: truthy\n\n  # Parameter naming\n  snapchat-path-param-naming:\n    description: Path parameters should use snake_case\n    message: \"Path parameter '{{value}}' should use snake_case\"\n    severity: info\n    given: \"$.paths[*][*].parameters[*][?(@.in\
  \ == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # Version prefix\n  snapchat-server-versioned:\n    description: Servers should include a versioned base path (v1, v2, v3)\n    message: \"Server URL should include an API version prefix\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/v[0-9]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/snapchat/refs/heads/main/rules/snapchat-rules.yml
tags:
- Advertising
- AR
- Augmented Reality
- Marketing
- Messaging
- Social Media
- Spectral
- Linting
- API Governance
---
