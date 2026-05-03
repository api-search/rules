---
api_specs:
- filename: trustwell-foodlogiq-openapi.yml
  format: yaml
  label: Trustwell FoodLogiQ API
  slug: trustwell-foodlogiq-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustwell/refs/heads/main/openapi/trustwell-foodlogiq-openapi.yml
categories:
- trustwell
description: Spectral linting rules defining API design standards and conventions for Trustwell.
layout: rules
name: Trustwell API Rules
provider_name: Trustwell
provider_slug: trustwell
rule_count: 10
rules:
- description: Trustwell operation IDs must use camelCase format.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustwell-operation-ids-camel-case
  severity: warn
- description: Trustwell API paths should be versioned with /v1/ prefix.
  given: $.paths
  name: trustwell-versioned-paths
  severity: warn
- description: All Trustwell API endpoints must require X-API-KEY authentication.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustwell-api-key-security
  severity: error
- description: Trustwell FoodLogiQ paths must use domain-specific prefixes for clarity.
  given: $.paths
  name: trustwell-domain-prefix-paths
  severity: info
- description: All Trustwell operations must have tags.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustwell-operations-tagged
  severity: warn
- description: GET operations must include a 200 response with JSON content.
  given: $.paths.*[get].responses.200
  name: trustwell-response-200-json
  severity: warn
- description: POST creation operations should return 201 status.
  given: $.paths.*[post]
  name: trustwell-post-201-response
  severity: info
- description: Date/time fields must use date-time format.
  given: $.components.schemas.*.properties[createdAt,updatedAt,resolvedAt]
  name: trustwell-date-time-format
  severity: warn
- description: Identifier fields (id, supplierId, etc.) must be string type.
  given: $.components.schemas.*.properties[id,supplierId,productId,incidentId,recallId]
  name: trustwell-id-string-type
  severity: warn
- description: Collection endpoints should support page and perPage pagination.
  given: $.paths.*[get]
  name: trustwell-pagination-params
  severity: info
rules_file: rules/trustwell-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trustwell/refs/heads/main/rules/trustwell-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 6
slug: trustwell-rules
source_filename: trustwell-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trustwell-operation-ids-camel-case:\n    description: Trustwell operation IDs must use camelCase format.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trustwell-versioned-paths:\n    description: Trustwell API paths should be versioned with /v1/ prefix.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  trustwell-api-key-security:\n    description: All Trustwell API endpoints must require X-API-KEY authentication.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  trustwell-domain-prefix-paths:\n    description: Trustwell FoodLogiQ paths must use domain-specific prefixes for clarity.\n    severity:\
  \ info\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/(suppliers|compliance|quality|products|traceability|recalls)\"\n\n  trustwell-operations-tagged:\n    description: All Trustwell operations must have tags.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  trustwell-response-200-json:\n    description: GET operations must include a 200 response with JSON content.\n    severity: warn\n    given: \"$.paths.*[get].responses.200\"\n    then:\n      field: content.application/json\n      function: truthy\n\n  trustwell-post-201-response:\n    description: POST creation operations should return 201 status.\n    severity: info\n    given: \"$.paths.*[post]\"\n    then:\n      field: responses.201\n      function: truthy\n\n  trustwell-date-time-format:\n    description: Date/time fields must use date-time format.\n    severity:\
  \ warn\n    given: \"$.components.schemas.*.properties[createdAt,updatedAt,resolvedAt]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  trustwell-id-string-type:\n    description: Identifier fields (id, supplierId, etc.) must be string type.\n    severity: warn\n    given: \"$.components.schemas.*.properties[id,supplierId,productId,incidentId,recallId]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  trustwell-pagination-params:\n    description: Collection endpoints should support page and perPage pagination.\n    severity: info\n    given: \"$.paths.*[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trustwell/refs/heads/main/rules/trustwell-rules.yml
tags:
- Food Industry
- Food Safety
- Nutrition
- Supply Chain
- Food Labeling
- Traceability
- Compliance
- Food Technology
- Spectral
- Linting
- API Governance
---
