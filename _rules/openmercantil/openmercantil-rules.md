---
api_specs:
- filename: openmercantil-openapi.yml
  format: yaml
  label: OpenMercantil Public API
  slug: openmercantil-public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/openapi/openmercantil-openapi.yml
categories:
- openmercantil
description: Spectral linting rules defining API design standards and conventions for OpenMercantil.
layout: rules
name: OpenMercantil API Rules
provider_name: OpenMercantil
provider_slug: openmercantil
rule_count: 9
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: openmercantil-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: openmercantil-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: openmercantil-summaries-title-case
  severity: warn
- description: Public paths must be versioned under /api/v1/
  given: $.paths[*]~
  name: openmercantil-v1-paths
  severity: error
- description: All public endpoints should document the 429 rate-limit response
  given: $.paths[*][get,post,put,delete].responses
  name: openmercantil-429-documented
  severity: warn
- description: Query parameters should use snake_case
  given: $.paths[*][*].parameters[?(@.in=='query')].name
  name: openmercantil-snake-case-query-params
  severity: info
- description: Company and person resource paths must use a `slug` path parameter
  given: $.paths[?(@property.match(/^\/api\/v1\/(company|person)\/.*/))][*].parameters[?(@.in=='path' && @.name=='slug')]
  name: openmercantil-slug-path-param
  severity: info
- description: 429 responses should document Retry-After and X-RateLimit-* headers
  given: $.paths[*][*].responses.429
  name: openmercantil-rate-limit-headers
  severity: warn
- description: Public read endpoints should not require authentication
  given: $.paths[?(@property.match(/^\/api\/v1\/(search|company|person|persona|daily|summary|cnae|sector|sectores|ccaa|sources|contracts|export|health)/))].get
  name: openmercantil-public-no-auth
  severity: info
rules_file: rules/openmercantil-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/rules/openmercantil-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 4
slug: openmercantil-rules
source_filename: openmercantil-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  openmercantil-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  openmercantil-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  openmercantil-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  openmercantil-v1-paths:\n    description: Public paths must be versioned under /api/v1/\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\
  ^/api/v1/.+$\"\n\n  openmercantil-429-documented:\n    description: All public endpoints should document the 429 rate-limit response\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  openmercantil-snake-case-query-params:\n    description: Query parameters should use snake_case\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in=='query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  openmercantil-slug-path-param:\n    description: Company and person resource paths must use a `slug` path parameter\n    severity: info\n    given: \"$.paths[?(@property.match(/^\\\\/api\\\\/v1\\\\/(company|person)\\\\/.*/))][*].parameters[?(@.in=='path' && @.name=='slug')]\"\n    then:\n      function: truthy\n\n  openmercantil-rate-limit-headers:\n    description: 429 responses should document Retry-After and X-RateLimit-* headers\n    severity:\
  \ warn\n    given: \"$.paths[*][*].responses.429\"\n    then:\n      field: headers\n      function: truthy\n\n  openmercantil-public-no-auth:\n    description: Public read endpoints should not require authentication\n    severity: info\n    given: \"$.paths[?(@property.match(/^\\\\/api\\\\/v1\\\\/(search|company|person|persona|daily|summary|cnae|sector|sectores|ccaa|sources|contracts|export|health)/))].get\"\n    then:\n      field: security\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/rules/openmercantil-rules.yml
tags:
- Open Data
- Spain
- Company Data
- Business Registry
- BORME
- Public Records
- Spanish Companies
- CIF
- CNAE
- Public Procurement
- PLACSP
- CNMV
- OEPM
- BDNS
- OpenSanctions
- Public-Interest Data
- Spanish Open Data
- REST API
- JSON
- CSV
- Geocoding
- Trust Score
- Registry Timeline
- Daily Summary
- Spectral
- Linting
- API Governance
---
