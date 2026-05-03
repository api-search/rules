---
api_specs:
- filename: restream-openapi.yml
  format: yaml
  label: Restream API
  slug: restream-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/restream/refs/heads/main/openapi/restream-openapi.yml
categories:
- restream
description: Spectral linting rules defining API design standards and conventions for Restream.
layout: rules
name: Restream API Rules
provider_name: Restream
provider_slug: restream
rule_count: 8
rules:
- description: All operations must have an operationId for SDK and documentation generation.
  given: $.paths[*][get,post,put,patch,delete]
  name: restream-operation-id-required
  severity: error
- description: All operations must have a summary for developer experience.
  given: $.paths[*][get,post,put,patch,delete]
  name: restream-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case per Restream API style.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: restream-summary-title-case
  severity: warn
- description: All operations must be tagged for grouping in the developer portal.
  given: $.paths[*][get,post,put,patch,delete]
  name: restream-tags-required
  severity: error
- description: OAuth2-secured operations must declare required scopes.
  given: $.paths[*][get,post,put,patch,delete].security[*].OAuth2
  name: restream-oauth2-scopes-documented
  severity: warn
- description: All operations must define a 200/201 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: restream-response-200-required
  severity: error
- description: API paths must use kebab-case for multi-word segments.
  given: $.paths[*]~
  name: restream-path-kebab-case
  severity: warn
- description: All paths must be prefixed with /v2 or use the OAuth token path.
  given: $.paths[*]~
  name: restream-v2-prefix
  severity: warn
rules_file: rules/restream-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/restream/refs/heads/main/rules/restream-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: restream-rules
source_filename: restream-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  restream-operation-id-required:\n    description: All operations must have an operationId for SDK and documentation generation.\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  restream-operation-summary-required:\n    description: All operations must have a summary for developer experience.\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  restream-summary-title-case:\n    description: Operation summaries must use Title Case per Restream API style.\n    message: \"Summary must use Title Case: '{{value}}'\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\
  \\s[A-Z][a-z]*)*$\"\n\n  restream-tags-required:\n    description: All operations must be tagged for grouping in the developer portal.\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  restream-oauth2-scopes-documented:\n    description: OAuth2-secured operations must declare required scopes.\n    message: \"OAuth2-secured operation must declare scopes\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].security[*].OAuth2\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  restream-response-200-required:\n    description: All operations must define a 200/201 success response.\n    message: \"Operation must have a success response (200 or 201)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  restream-path-kebab-case:\n    description: API paths must use kebab-case for multi-word segments.\n    message: \"Path segment must use kebab-case: '{{value}}'\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+((/[a-z0-9{}-]+)*)?)$\"\n\n  restream-v2-prefix:\n    description: All paths must be prefixed with /v2 or use the OAuth token path.\n    message: \"Path must begin with /v2 or /oauth\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(v2|oauth)/\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/restream/refs/heads/main/rules/restream-rules.yml
tags:
- Broadcast
- Chat
- Content Delivery
- Live Streaming
- Multistreaming
- Video Streaming
- Spectral
- Linting
- API Governance
---
