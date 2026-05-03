---
api_specs:
- filename: trustradius-public-openapi.yml
  format: yaml
  label: TrustRadius Public API
  slug: trustradius-public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustradius/refs/heads/main/openapi/trustradius-public-openapi.yml
- filename: trustradius-reviews-openapi.yml
  format: yaml
  label: TrustRadius Reviews API
  slug: trustradius-reviews-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustradius/refs/heads/main/openapi/trustradius-reviews-openapi.yml
categories:
- trustradius
description: Spectral linting rules defining API design standards and conventions for TrustRadius.
layout: rules
name: TrustRadius API Rules
provider_name: TrustRadius
provider_slug: trustradius
rule_count: 9
rules:
- description: TrustRadius operation IDs must use camelCase format.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustradius-operation-ids-camel-case
  severity: warn
- description: All TrustRadius API paths must include version (e.g., /v1/).
  given: $.paths
  name: trustradius-versioned-paths
  severity: error
- description: All TrustRadius API operations must require API key authentication.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustradius-api-key-security
  severity: error
- description: All TrustRadius operations must have tags.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustradius-operations-tagged
  severity: warn
- description: TrustRadius path parameters for products, categories, and companies use slug format.
  given: $.paths
  name: trustradius-slug-path-params
  severity: warn
- description: TrustRadius trScore fields must define minimum 1 and maximum 10 range.
  given: $.components.schemas.*.properties.trScore
  name: trustradius-trscore-range
  severity: warn
- description: TrustRadius GET operations must include a 200 response with JSON content.
  given: $.paths.*[get].responses.200
  name: trustradius-response-200-json
  severity: warn
- description: TrustRadius collection endpoints should support page and perPage parameters.
  given: $.paths.*[get]
  name: trustradius-pagination-params
  severity: info
- description: Date/time fields in TrustRadius schemas must use date-time format.
  given: $.components.schemas.*.properties[createdAt,updatedAt]
  name: trustradius-date-time-format
  severity: warn
rules_file: rules/trustradius-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trustradius/refs/heads/main/rules/trustradius-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: trustradius-rules
source_filename: trustradius-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trustradius-operation-ids-camel-case:\n    description: TrustRadius operation IDs must use camelCase format.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trustradius-versioned-paths:\n    description: All TrustRadius API paths must include version (e.g., /v1/).\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  trustradius-api-key-security:\n    description: All TrustRadius API operations must require API key authentication.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  trustradius-operations-tagged:\n    description: All TrustRadius operations must have tags.\n    severity: warn\n    given:\
  \ \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  trustradius-slug-path-params:\n    description: TrustRadius path parameters for products, categories, and companies use slug format.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/[a-z-]+(/(\\\\{[a-z]+Slug\\\\}|[a-z-]+))*(/[a-z-]+)?\"\n\n  trustradius-trscore-range:\n    description: TrustRadius trScore fields must define minimum 1 and maximum 10 range.\n    severity: warn\n    given: \"$.components.schemas.*.properties.trScore\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            minimum:\n              const: 1\n            maximum:\n              const: 10\n\n  trustradius-response-200-json:\n    description: TrustRadius GET operations must include a 200 response with JSON content.\n    severity: warn\n    given: \"$.paths.*[get].responses.200\"\
  \n    then:\n      field: content.application/json\n      function: truthy\n\n  trustradius-pagination-params:\n    description: TrustRadius collection endpoints should support page and perPage parameters.\n    severity: info\n    given: \"$.paths.*[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n\n  trustradius-date-time-format:\n    description: Date/time fields in TrustRadius schemas must use date-time format.\n    severity: warn\n    given: \"$.components.schemas.*.properties[createdAt,updatedAt]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trustradius/refs/heads/main/rules/trustradius-rules.yml
tags:
- B2B Software Reviews
- Buyer Intelligence
- Intent Data
- Software Reviews
- Reviews
- Product Reviews
- Categories
- Spectral
- Linting
- API Governance
---
