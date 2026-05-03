---
api_specs:
- filename: ticketmaster-discovery-openapi.yml
  format: yaml
  label: Ticketmaster Discovery API
  slug: ticketmaster-discovery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ticketmaster/refs/heads/main/openapi/ticketmaster-discovery-openapi.yml
- filename: ticketmaster-commerce-openapi.yml
  format: yaml
  label: Ticketmaster Commerce API
  slug: ticketmaster-commerce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ticketmaster/refs/heads/main/openapi/ticketmaster-commerce-openapi.yml
categories:
- ticketmaster
description: Spectral linting rules defining API design standards and conventions for Ticketmaster.
layout: rules
name: Ticketmaster API Rules
provider_name: Ticketmaster
provider_slug: ticketmaster
rule_count: 11
rules:
- description: Ticketmaster Discovery API paths must end with .json
  given: $.paths[*]~
  name: ticketmaster-paths-json-suffix
  severity: warn
- description: All operations must accept an apikey query parameter
  given: $.paths[*][get,post,put,delete]
  name: ticketmaster-apikey-param-required
  severity: error
- description: All tags must use Title Case
  given: $.tags[*].name
  name: ticketmaster-tags-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: ticketmaster-operation-ids-camel-case
  severity: warn
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: ticketmaster-responses-200-on-get
  severity: error
- description: GET operations should document 401 unauthorized response
  given: $.paths[*].get
  name: ticketmaster-responses-401-on-get
  severity: info
- description: Single resource GET endpoints should document 404 response
  given: $.paths[?(/\{.*\}/)].get
  name: ticketmaster-responses-404-on-resource
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: ticketmaster-servers-https-only
  severity: error
- description: List operations should support size and page parameters
  given: $.paths[*~$(\.json)].get.parameters
  name: ticketmaster-pagination-in-list-ops
  severity: info
- description: Collection responses should use HAL _embedded structure
  given: $.components.schemas[?(@.properties._embedded)]
  name: ticketmaster-embedded-response-structure
  severity: info
- description: API version should be documented
  given: $.info
  name: ticketmaster-info-version-semver
  severity: warn
rules_file: rules/ticketmaster-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ticketmaster/refs/heads/main/rules/ticketmaster-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 4
  warn: 4
slug: ticketmaster-rules
source_filename: ticketmaster-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  ticketmaster-paths-json-suffix:\n    description: Ticketmaster Discovery API paths must end with .json\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^.*\\\\.json$\"\n\n  ticketmaster-apikey-param-required:\n    description: All operations must accept an apikey query parameter\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: parameters\n      function: defined\n\n  ticketmaster-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]+$\"\n\n  ticketmaster-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n      \
  \  match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  ticketmaster-responses-200-on-get:\n    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  ticketmaster-responses-401-on-get:\n    description: GET operations should document 401 unauthorized response\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.401\n      function: defined\n\n  ticketmaster-responses-404-on-resource:\n    description: Single resource GET endpoints should document 404 response\n    severity: info\n    given: \"$.paths[?(/\\\\{.*\\\\}/)].get\"\n    then:\n      field: responses.404\n      function: defined\n\n  ticketmaster-servers-https-only:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  ticketmaster-pagination-in-list-ops:\n\
  \    description: List operations should support size and page parameters\n    severity: info\n    given: \"$.paths[*~$(\\\\.json)].get.parameters\"\n    then:\n      function: defined\n\n  ticketmaster-embedded-response-structure:\n    description: Collection responses should use HAL _embedded structure\n    severity: info\n    given: \"$.components.schemas[?(@.properties._embedded)]\"\n    then:\n      field: properties._embedded\n      function: defined\n\n  ticketmaster-info-version-semver:\n    description: API version should be documented\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: version\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ticketmaster/refs/heads/main/rules/ticketmaster-rules.yml
tags:
- Commerce
- Concerts
- Entertainment
- Events
- Sports
- Tickets
- Venues
- Spectral
- Linting
- API Governance
---
