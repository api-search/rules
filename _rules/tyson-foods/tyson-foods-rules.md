---
api_specs:
- filename: tyson-foods-edi-integration-api-openapi.yml
  format: yaml
  label: Tyson Foods EDI Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tyson-foods/refs/heads/main/openapi/tyson-foods-edi-integration-api-openapi.yml
categories:
- tyson
description: Spectral linting rules defining API design standards and conventions for Tyson Foods.
layout: rules
name: Tyson Foods API Rules
provider_name: Tyson Foods
provider_slug: tyson-foods
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tyson-foods-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tyson-foods-operation-id-camel-case
  severity: warn
- description: All Tyson Foods API operations should require authentication
  given: $.paths[*][get,post,put,patch,delete]
  name: tyson-foods-auth-required
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: tyson-foods-operation-description
  severity: warn
- description: Path parameters should have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: tyson-foods-path-param-description
  severity: hint
- description: Operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tyson-foods-success-response
  severity: error
- description: Tags must use Title Case
  given: $.tags[*].name
  name: tyson-foods-tags-title-case
  severity: warn
- description: API servers should use HTTPS
  given: $.servers[*].url
  name: tyson-foods-server-https
  severity: error
rules_file: rules/tyson-foods-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tyson-foods/refs/heads/main/rules/tyson-foods-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 5
slug: tyson-foods-rules
source_filename: tyson-foods-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # All summaries must use Title Case\n  tyson-foods-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operation IDs must use camelCase\n  tyson-foods-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations should have authentication\n  tyson-foods-auth-required:\n    description: All Tyson Foods API operations should require authentication\n    message: \"Operation should declare authentication security\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    severity: warn\n    then:\n      field: security\n      function: truthy\n\n  # All operations should have descriptions\n  tyson-foods-operation-description:\n    description: All operations should have a description\n    message: \"Operation '{{path}}' is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # Path parameters should have descriptions\n  tyson-foods-path-param-description:\n    description: Path parameters should have descriptions\n    message: \"Path parameter '{{value}}' is missing description\"\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    severity: hint\n    then:\n      field: description\n      function: truthy\n\n  # Successful responses must be defined\n  tyson-foods-success-response:\n    description: Operations must define a success response\n    message: \"Operation must define a 200 or 201 response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # Tags should use Title Case\n  tyson-foods-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  # Server URLs should use HTTPS\n  tyson-foods-server-https:\n    description: API servers should use HTTPS\n    message: \"Server URL '{{value}}' should use HTTPS\"\n    given: \"$.servers[*].url\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tyson-foods/refs/heads/main/rules/tyson-foods-rules.yml
tags:
- B2B Integration
- EDI
- Food
- Fortune 100
- Supply Chain
- Spectral
- Linting
- API Governance
---
