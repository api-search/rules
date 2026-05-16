---
api_specs:
- filename: brewpage-openapi.yml
  format: yaml
  label: BrewPage API
  slug: api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/brewpage/refs/heads/main/openapi/brewpage-openapi.yml
categories:
- brewpage
description: Spectral linting rules defining API design standards and conventions for BrewPage.
layout: rules
name: BrewPage API Rules
provider_name: BrewPage
provider_slug: brewpage
rule_count: 21
rules:
- description: All BrewPage OpenAPI titles SHOULD start with "BrewPage ".
  given: $.info.title
  name: brewpage-info-title-prefix
  severity: warn
- description: All BrewPage API servers MUST use HTTPS.
  given: $.servers[*].url
  name: brewpage-server-https
  severity: error
- description: BrewPage servers SHOULD be brewpage.app or brewdata.app.
  given: $.servers[*].url
  name: brewpage-server-host
  severity: warn
- description: BrewPage REST endpoints SHOULD live under /api/, /preview/, /preview-html/, or be public short-link paths (/{ns}/{id}).
  given: $.paths[*]~
  name: brewpage-base-path-api
  severity: warn
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: brewpage-operation-id-required
  severity: error
- description: operationId SHOULD be camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: brewpage-operation-id-camel-case
  severity: warn
- description: Operations MUST have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: brewpage-summary-required
  severity: error
- description: Operation summaries SHOULD begin with "BrewPage ".
  given: $.paths[*][get,post,put,delete,patch].summary
  name: brewpage-summary-prefix
  severity: warn
- description: Operation summaries SHOULD start with a capital letter (Title Case).
  given: $.paths[*][get,post,put,delete,patch].summary
  name: brewpage-summary-title-case
  severity: warn
- description: Operations SHOULD have a description.
  given: $.paths[*][get,post,put,delete,patch]
  name: brewpage-description-required
  severity: warn
- description: Operations MUST be tagged with at least one tag.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: brewpage-tags-required
  severity: warn
- description: BrewPage `ns` path parameters SHOULD enforce the kebab-case 1..32 char pattern.
  given: $.paths.*.*.parameters[?(@.name=='ns' && @.in=='path')].schema
  name: brewpage-namespace-pattern
  severity: warn
- description: BrewPage schema properties SHOULD use camelCase (matches API payloads like ownerToken, ownerLink, ttlDays).
  given: $.components.schemas[*].properties[*]~
  name: brewpage-camel-case-properties
  severity: warn
- description: Tags SHOULD use Title Case names.
  given: $.tags[*].name
  name: brewpage-tag-title-case
  severity: warn
- description: Tags SHOULD have a description.
  given: $.tags[*]
  name: brewpage-tag-description
  severity: warn
- description: BrewPage requires a User-Agent header — operations SHOULD declare the parameter or describe it.
  given: $.paths[*][get,post,put,delete,patch]
  name: brewpage-user-agent-header
  severity: info
- description: Mutations SHOULD authenticate via the `X-Owner-Token` header (not query string or body).
  given: $.paths[*][put,delete].parameters[?(@.in=='header')].name
  name: brewpage-owner-token-header-name
  severity: warn
- description: Operations MUST define a 2xx response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: brewpage-success-response
  severity: error
- description: Mutating operations SHOULD document 403 (wrong owner token) and 404 responses.
  given: $.paths[*][put,delete].responses
  name: brewpage-error-responses
  severity: warn
- description: TTL parameters SHOULD bound 1..30 days to match BrewPage's published retention window.
  given: $.paths[*][post].parameters[?(@.name=='ttl' || @.name=='ttl_days')]
  name: brewpage-ttl-bounds
  severity: info
- description: BrewPage short ids are 10-char base32-like strings — descriptions SHOULD note this where the `id` path parameter appears.
  given: $.paths.*.*.parameters[?(@.name=='id' && @.in=='path')]
  name: brewpage-short-id-length
  severity: info
rules_file: rules/brewpage-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/brewpage/refs/heads/main/rules/brewpage-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 3
  warn: 14
slug: brewpage-rules
source_filename: brewpage-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  brewpage-info-title-prefix:\n    description: All BrewPage OpenAPI titles SHOULD start with \"BrewPage \".\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: '^BrewPage '\n  brewpage-server-https:\n    description: All BrewPage API servers MUST use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://'\n  brewpage-server-host:\n    description: BrewPage servers SHOULD be brewpage.app or brewdata.app.\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: '^https://(brewpage|brewdata)\\.app'\n  brewpage-base-path-api:\n    description: BrewPage REST endpoints SHOULD live under /api/, /preview/, /preview-html/, or be public short-link paths (/{ns}/{id}).\n    severity: warn\n    given: $.paths[*]~\n    then:\n  \
  \    function: pattern\n      functionOptions:\n        match: '^(/api/|/preview/|/preview-html/|/\\{|/[a-z0-9-]+\\.txt$)'\n  brewpage-operation-id-required:\n    description: Operations MUST have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n  brewpage-operation-id-camel-case:\n    description: operationId SHOULD be camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9_]*$'\n  brewpage-summary-required:\n    description: Operations MUST have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n  brewpage-summary-prefix:\n    description: Operation summaries SHOULD begin with \"BrewPage \".\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: '^BrewPage '\n  brewpage-summary-title-case:\n    description: Operation summaries SHOULD start with a capital letter (Title Case).\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z]'\n  brewpage-description-required:\n    description: Operations SHOULD have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n  brewpage-tags-required:\n    description: Operations MUST be tagged with at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].tags\n    then:\n      function: truthy\n  brewpage-namespace-pattern:\n    description: BrewPage `ns` path parameters SHOULD enforce the kebab-case 1..32 char pattern.\n    severity: warn\n    given: $.paths.*.*.parameters[?(@.name=='ns' && @.in=='path')].schema\n\
  \    then:\n      field: pattern\n      function: truthy\n  brewpage-camel-case-properties:\n    description: BrewPage schema properties SHOULD use camelCase (matches API payloads like ownerToken, ownerLink, ttlDays).\n    severity: warn\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n  brewpage-tag-title-case:\n    description: Tags SHOULD use Title Case names.\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z0-9 -]*$'\n  brewpage-tag-description:\n    description: Tags SHOULD have a description.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n  brewpage-user-agent-header:\n    description: BrewPage requires a User-Agent header — operations SHOULD declare the parameter or describe it.\n    severity: info\n    given: $.paths[*][get,post,put,delete,patch]\n\
  \    then:\n      field: parameters\n      function: truthy\n  brewpage-owner-token-header-name:\n    description: Mutations SHOULD authenticate via the `X-Owner-Token` header (not query string or body).\n    severity: warn\n    given: $.paths[*][put,delete].parameters[?(@.in=='header')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(X-Owner-Token|X-Password|User-Agent|Content-Type)$'\n  brewpage-success-response:\n    description: Operations MUST define a 2xx response.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            '^2[0-9][0-9]$':\n              type: object\n          additionalProperties: true\n  brewpage-error-responses:\n    description: Mutating operations SHOULD document 403 (wrong owner token) and 404 responses.\n    severity: warn\n    given: $.paths[*][put,delete].responses\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['404']\n  brewpage-ttl-bounds:\n    description: TTL parameters SHOULD bound 1..30 days to match BrewPage's published retention window.\n    severity: info\n    given: $.paths[*][post].parameters[?(@.name=='ttl' || @.name=='ttl_days')]\n    then:\n      field: schema\n      function: truthy\n  brewpage-short-id-length:\n    description: BrewPage short ids are 10-char base32-like strings — descriptions SHOULD note this where the `id` path parameter appears.\n    severity: info\n    given: $.paths.*.*.parameters[?(@.name=='id' && @.in=='path')]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/brewpage/refs/heads/main/rules/brewpage-rules.yml
tags:
- Hosting
- Markdown
- HTML
- AI Artifacts
- File Hosting
- Developer Tools
- Spectral
- Linting
- API Governance
---
