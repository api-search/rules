---
api_specs:
- filename: seatgeek-platform-openapi.yml
  format: yaml
  label: SeatGeek Platform API
  slug: seatgeek-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seatgeek/refs/heads/main/openapi/seatgeek-platform-openapi.yml
categories:
- seatgeek
description: Spectral linting rules defining API design standards and conventions for SeatGeek.
layout: rules
name: SeatGeek API Rules
provider_name: SeatGeek
provider_slug: seatgeek
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: seatgeek-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: seatgeek-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: seatgeek-summaries-title-case
  severity: warn
- description: Collection endpoints should support per_page and page parameters
  given: $.paths[*][get]
  name: seatgeek-pagination-parameters
  severity: warn
- description: Platform API is read-only and should only use GET methods
  given: $.paths[*]
  name: seatgeek-get-only-read-api
  severity: info
- description: Collection responses should include meta pagination object
  given: $.paths[*][get].responses['200'].content['application/json'].schema.properties
  name: seatgeek-response-meta
  severity: info
- description: All endpoints require client_id authentication
  given: $.paths[*][*]
  name: seatgeek-client-id-security
  severity: error
- description: Collection paths should use plural nouns
  given: $.paths
  name: seatgeek-path-plural-nouns
  severity: warn
rules_file: rules/seatgeek-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/seatgeek/refs/heads/main/rules/seatgeek-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: seatgeek-rules
source_filename: seatgeek-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  seatgeek-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  seatgeek-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  seatgeek-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  seatgeek-pagination-parameters:\n    description: Collection endpoints should support per_page and page parameters\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: parameters\n      function: truthy\n\n\
  \  seatgeek-get-only-read-api:\n    description: Platform API is read-only and should only use GET methods\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(post|put|patch|delete)$\"\n\n  seatgeek-response-meta:\n    description: Collection responses should include meta pagination object\n    severity: info\n    given: \"$.paths[*][get].responses['200'].content['application/json'].schema.properties\"\n    then:\n      field: meta\n      function: truthy\n\n  seatgeek-client-id-security:\n    description: All endpoints require client_id authentication\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  seatgeek-path-plural-nouns:\n    description: Collection paths should use plural nouns\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(events|performers|venues|taxonomies|recommendations)\"\
  \n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/seatgeek/refs/heads/main/rules/seatgeek-rules.yml
tags:
- Events
- Tickets
- Live Events
- Concerts
- Sports
- Venues
- Ticketing
- Spectral
- Linting
- API Governance
---
