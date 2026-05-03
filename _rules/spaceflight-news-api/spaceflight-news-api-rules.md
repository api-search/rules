---
api_specs:
- filename: spaceflight-news-api-openapi.yml
  format: yaml
  label: Spaceflight News API
  slug: spaceflight-news-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spaceflight-news-api/refs/heads/main/openapi/spaceflight-news-api-openapi.yml
categories:
- snapi
description: Spectral linting rules defining API design standards and conventions for Spaceflight News API.
layout: rules
name: Spaceflight News API API Rules
provider_name: Spaceflight News API
provider_slug: spaceflight-news-api
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: snapi-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: snapi-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: snapi-tags-title-case
  severity: warn
- description: SpaceAPI Django-based paths use trailing slashes
  given: $.paths[*]~
  name: snapi-paths-trailing-slash
  severity: info
- description: List endpoints should have limit and offset parameters
  given: $.paths[*].get
  name: snapi-list-endpoints-have-pagination
  severity: warn
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: snapi-response-must-have-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: snapi-schema-properties-have-descriptions
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: snapi-servers-must-be-https
  severity: error
- description: API base path should include version prefix
  given: $.servers[*].url
  name: snapi-api-versioned-path
  severity: info
rules_file: rules/spaceflight-news-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spaceflight-news-api/refs/heads/main/rules/spaceflight-news-api-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 5
slug: spaceflight-news-api-rules
source_filename: spaceflight-news-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  snapi-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*)(\\\\s[A-Z][a-z0-9]*)*$\"\n\n  snapi-operation-id-camel-case:\n    description: All operationIds must use camelCase\n    message: OperationId \"{{value}}\" must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  snapi-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*)(\\\\s[A-Z][a-z0-9]*)*$\"\n\n  snapi-paths-trailing-slash:\n\
  \    description: SpaceAPI Django-based paths use trailing slashes\n    message: Path \"{{value}}\" should end with a trailing slash\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/$\"\n\n  snapi-list-endpoints-have-pagination:\n    description: List endpoints should have limit and offset parameters\n    message: List endpoint must include limit and offset query parameters\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  snapi-response-must-have-description:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  snapi-schema-properties-have-descriptions:\n    description: Schema properties should have descriptions\n    message: Schema property \"{{path}}\" should have\
  \ a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  snapi-servers-must-be-https:\n    description: All server URLs must use HTTPS\n    message: Server URL \"{{value}}\" must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  snapi-api-versioned-path:\n    description: API base path should include version prefix\n    message: Server URL should include API version (e.g., /v4)\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spaceflight-news-api/refs/heads/main/rules/spaceflight-news-api-rules.yml
tags:
- News
- Space
- Spaceflight
- Media
- Spectral
- Linting
- API Governance
---
