---
api_specs:
- filename: zdnet-rss.yml
  format: yaml
  label: ZDNet RSS Feed
  slug: rss
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zdnet/refs/heads/main/openapi/zdnet-rss.yml
categories:
- info
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for ZDNet.
layout: rules
name: ZDNet API Rules
provider_name: ZDNet
provider_slug: zdnet
rule_count: 18
rules:
- description: API title is required
  given: $.info
  name: info-title-required
  severity: error
- description: API description is required
  given: $.info
  name: info-description-required
  severity: warn
- description: API version is required
  given: $.info
  name: info-version-required
  severity: error
- description: API contact is required
  given: $.info
  name: info-contact-required
  severity: warn
- description: OpenAPI version should be 3.x
  given: $
  name: openapi-version-3
  severity: warn
- description: Servers must be defined
  given: $
  name: servers-required
  severity: error
- description: Server URLs should use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Path segments should be kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Operation summary is required
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: warn
- description: Operation description is required
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: operationId is required
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId-required
  severity: error
- description: Operation tags are required
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Operation summary should start with "ZDNet"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix-zdnet
  severity: warn
- description: Parameters need a description
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define a 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-2xx-required
  severity: error
- description: Top-level schemas need a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Security schemes should be defined
  given: $.components
  name: security-schemes-defined
  severity: warn
rules_file: rules/zdnet-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/zdnet/refs/heads/main/rules/zdnet-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 13
slug: zdnet-rules
source_filename: zdnet-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  info-title-required:\n    description: API title is required\n    message: '{{property}} is required'\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n  info-description-required:\n    description: API description is required\n    message: '{{property}} is required'\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n  info-version-required:\n    description: API version is required\n    message: '{{property}} is required'\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n  info-contact-required:\n    description: API contact is required\n    message: '{{property}} is required'\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n  openapi-version-3:\n    description: OpenAPI version should be 3.x\n    message: Use OpenAPI 3.x\n    severity: warn\n    given: $\n    then:\n      field:\
  \ openapi\n      function: pattern\n      functionOptions:\n        match: ^3\\.\n  servers-required:\n    description: Servers must be defined\n    message: Define servers\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n  servers-https:\n    description: Server URLs should use HTTPS\n    message: Use HTTPS\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: ^https://\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: Remove trailing slash\n    severity: warn\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        notMatch: .+/$\n  paths-kebab-case:\n    description: Path segments should be kebab-case\n    message: Use kebab-case\n    severity: warn\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n       \
  \ match: ^(/[a-z0-9-]+|/\\{[a-zA-Z][a-zA-Z0-9_]*\\})+/?$\n  operation-summary-required:\n    description: Operation summary is required\n    message: Add a summary\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n  operation-description-required:\n    description: Operation description is required\n    message: Add a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n  operation-operationId-required:\n    description: operationId is required\n    message: Add operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n  operation-tags-required:\n    description: Operation tags are required\n    message: Add tags\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\
  \  operation-summary-prefix-zdnet:\n    description: Operation summary should start with \"ZDNet\"\n    message: Summary should start with \"ZDNet\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: ^ZDNet\n  parameter-description-required:\n    description: Parameters need a description\n    message: Add a description\n    severity: warn\n    given: $.paths[*][*].parameters[*]\n    then:\n      field: description\n      function: truthy\n  response-2xx-required:\n    description: Operations must define a 2xx success response\n    message: Add a 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: pattern\n      functionOptions:\n        match: ^[23]\n      field: '@key'\n  schema-description-required:\n    description: Top-level schemas need a description\n    message: Add a description\n    severity: warn\n    given:\
  \ $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n  security-schemes-defined:\n    description: Security schemes should be defined\n    message: Define securitySchemes\n    severity: warn\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zdnet/refs/heads/main/rules/zdnet-rules.yml
tags:
- Enterprise IT
- Media
- Technology News
- Spectral
- Linting
- API Governance
---
