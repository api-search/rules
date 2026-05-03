---
api_specs:
- filename: yoast-rest-openapi.yml
  format: yaml
  label: Yoast REST API
  slug: yoast-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/yoast/refs/heads/main/openapi/yoast-rest-openapi.yml
categories:
- yoast
description: Spectral linting rules defining API design standards and conventions for Yoast.
layout: rules
name: Yoast API Rules
provider_name: Yoast
provider_slug: yoast
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: yoast-operation-summary-title-case
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: yoast-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: yoast-all-operations-have-tags
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: yoast-all-operations-have-description
  severity: warn
- description: All response objects should have descriptions
  given: $.paths[*][*].responses[*]
  name: yoast-responses-have-descriptions
  severity: warn
- description: All parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: yoast-parameters-have-descriptions
  severity: warn
- description: GET operations should not have request bodies
  given: $.paths[*].get
  name: yoast-get-read-only
  severity: error
- description: Yoast custom endpoints should use /yoast/v1/ prefix
  given: $.paths
  name: yoast-v1-path-prefix
  severity: hint
rules_file: rules/yoast-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/yoast/refs/heads/main/rules/yoast-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 6
slug: yoast-rules
source_filename: yoast-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  yoast-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n    severity: warn\n\n  yoast-operation-ids-camel-case:\n    description: Operation IDs should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n    severity: warn\n\n  yoast-all-operations-have-tags:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  yoast-all-operations-have-description:\n   \
  \ description: All operations must have a description\n    message: \"Operation must have a description\"\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  yoast-responses-have-descriptions:\n    description: All response objects should have descriptions\n    message: \"Response must have a description\"\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  yoast-parameters-have-descriptions:\n    description: All parameters should have descriptions\n    message: \"Parameter must have a description\"\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  yoast-get-read-only:\n    description: GET operations should not have request bodies\n    message: \"GET operation '{{path}}' should not have a requestBody\"\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n\
  \      function: falsy\n    severity: error\n\n  yoast-v1-path-prefix:\n    description: Yoast custom endpoints should use /yoast/v1/ prefix\n    message: \"Custom Yoast paths should start with /yoast/v1/\"\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^/yoast/\":\n              type: object\n    severity: hint\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/yoast/refs/heads/main/rules/yoast-rules.yml
tags:
- SEO
- WordPress
- Content Optimization
- Schema
- Metadata
- Spectral
- Linting
- API Governance
---
