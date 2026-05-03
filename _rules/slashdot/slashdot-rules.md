---
api_specs:
- filename: slashdot-rss-openapi.yml
  format: yaml
  label: Slashdot RSS/Atom Feeds
  slug: rss-feeds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/slashdot/refs/heads/main/openapi/slashdot-rss-openapi.yml
categories:
- slashdot
description: Spectral linting rules defining API design standards and conventions for Slashdot.
layout: rules
name: Slashdot API Rules
provider_name: Slashdot
provider_slug: slashdot
rule_count: 5
rules:
- description: All feed operations must have a descriptive Title Case summary
  given: $.paths[*][get].summary
  name: slashdot-feed-operation-summary
  severity: warn
- description: All feed operations must include the Feeds tag
  given: $.paths[*][get].tags
  name: slashdot-feed-tag-required
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: slashdot-response-200-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get].operationId
  name: slashdot-operation-id-camel-case
  severity: warn
- description: RSS feed responses must declare application/rss+xml content type
  given: $.paths[*].get.responses.200.content
  name: slashdot-rss-content-type
  severity: warn
rules_file: rules/slashdot-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/slashdot/refs/heads/main/rules/slashdot-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 4
slug: slashdot-rules
source_filename: slashdot-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  slashdot-feed-operation-summary:\n    description: All feed operations must have a descriptive Title Case summary\n    message: 'Operation summary must be present and use Title Case'\n    severity: warn\n    given: '$.paths[*][get].summary'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9 ()/-]*$'\n\n  slashdot-feed-tag-required:\n    description: All feed operations must include the Feeds tag\n    message: 'Operations must include the \"Feeds\" tag'\n    severity: warn\n    given: '$.paths[*][get].tags'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: string\n            pattern: '^Feeds$'\n\n  slashdot-response-200-required:\n    description: All GET operations must define a 200 response\n    message: 'GET operations must define a 200 OK response'\n    severity: error\n    given: '$.paths[*].get.responses'\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '200'\n\n  slashdot-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: 'operationId must use camelCase (e.g., getMainFeed not get_main_feed)'\n    severity: warn\n    given: '$.paths[*][get].operationId'\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  slashdot-rss-content-type:\n    description: RSS feed responses must declare application/rss+xml content type\n    message: 'RSS feed responses should declare application/rss+xml content type'\n    severity: warn\n    given: '$.paths[*].get.responses.200.content'\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/slashdot/refs/heads/main/rules/slashdot-rules.yml
tags:
- Media
- Open Source
- Technology News
- RSS
- Spectral
- Linting
- API Governance
---
