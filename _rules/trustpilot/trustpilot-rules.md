---
api_specs:
- filename: trustpilot-business-units-openapi.yml
  format: yaml
  label: Trustpilot Business Units API
  slug: trustpilot-business-units-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/openapi/trustpilot-business-units-openapi.yml
- filename: trustpilot-service-reviews-openapi.yml
  format: yaml
  label: Trustpilot Service Reviews API
  slug: trustpilot-service-reviews-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/openapi/trustpilot-service-reviews-openapi.yml
- filename: trustpilot-invitation-openapi.yml
  format: yaml
  label: Trustpilot Invitation API
  slug: trustpilot-invitation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/openapi/trustpilot-invitation-openapi.yml
- filename: trustpilot-product-reviews-openapi.yml
  format: yaml
  label: Trustpilot Product Reviews API
  slug: trustpilot-product-reviews-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/openapi/trustpilot-product-reviews-openapi.yml
categories:
- trustpilot
description: Spectral linting rules defining API design standards and conventions for Trustpilot.
layout: rules
name: Trustpilot API Rules
provider_name: Trustpilot
provider_slug: trustpilot
rule_count: 11
rules:
- description: Trustpilot operation IDs must use camelCase format.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustpilot-operation-ids-camel-case
  severity: warn
- description: All Trustpilot API paths must be versioned with /v1/ prefix.
  given: $.paths
  name: trustpilot-path-versioned
  severity: error
- description: Trustpilot private endpoints (/v1/private/*) must require OAuth2 security.
  given: $.paths['/v1/private/*'].*[get,post,put,patch,delete]
  name: trustpilot-private-paths-require-oauth
  severity: error
- description: Trustpilot public endpoints should define API key authentication.
  given: $.paths[?(!@property.startsWith('/v1/private/'))].*[get,post,put,patch,delete].parameters[?(@.name=='apikey')]
  name: trustpilot-public-paths-require-apikey
  severity: warn
- description: Business unit endpoints must use {businessUnitId} path parameter.
  given: $.paths[?(@property.includes('business-units'))]
  name: trustpilot-business-unit-id-in-path
  severity: warn
- description: Review-specific endpoints must use {reviewId} path parameter.
  given: $.paths[?(@property.includes('reviews') && !@property.endsWith('/reviews'))]
  name: trustpilot-review-id-in-path
  severity: warn
- description: Star rating fields must be integer type with min 1, max 5.
  given: $.components.schemas.*.properties.stars
  name: trustpilot-stars-integer
  severity: warn
- description: GET operations must define a 200 response.
  given: $.paths.*[get]
  name: trustpilot-responses-have-200
  severity: warn
- description: Date/time fields in Trustpilot schemas must use date-time format.
  given: $.components.schemas.*.properties[createdAt,updatedAt,preferredSendTime]
  name: trustpilot-date-time-format
  severity: warn
- description: All Trustpilot operations should be tagged.
  given: $.paths.*[get,post,put,patch,delete]
  name: trustpilot-operations-have-tags
  severity: warn
- description: Trustpilot path segments must use kebab-case.
  given: $.paths
  name: trustpilot-kebab-case-paths
  severity: warn
rules_file: rules/trustpilot-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/rules/trustpilot-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 9
slug: trustpilot-rules
source_filename: trustpilot-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trustpilot-operation-ids-camel-case:\n    description: Trustpilot operation IDs must use camelCase format.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trustpilot-path-versioned:\n    description: All Trustpilot API paths must be versioned with /v1/ prefix.\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  trustpilot-private-paths-require-oauth:\n    description: Trustpilot private endpoints (/v1/private/*) must require OAuth2 security.\n    severity: error\n    given: \"$.paths['/v1/private/*'].*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  trustpilot-public-paths-require-apikey:\n    description: Trustpilot public endpoints should\
  \ define API key authentication.\n    severity: warn\n    given: \"$.paths[?(!@property.startsWith('/v1/private/'))].*[get,post,put,patch,delete].parameters[?(@.name=='apikey')]\"\n    then:\n      field: required\n      function: truthy\n\n  trustpilot-business-unit-id-in-path:\n    description: Business unit endpoints must use {businessUnitId} path parameter.\n    severity: warn\n    given: \"$.paths[?(@property.includes('business-units'))]\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"\\\\{businessUnitId\\\\}|/search\"\n\n  trustpilot-review-id-in-path:\n    description: Review-specific endpoints must use {reviewId} path parameter.\n    severity: warn\n    given: \"$.paths[?(@property.includes('reviews') && !@property.endsWith('/reviews'))]\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"\\\\{reviewId\\\\}|summaries|attribute-summaries|batch-summaries|latest|invitation-links\"\
  \n\n  trustpilot-stars-integer:\n    description: Star rating fields must be integer type with min 1, max 5.\n    severity: warn\n    given: \"$.components.schemas.*.properties.stars\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  trustpilot-responses-have-200:\n    description: GET operations must define a 200 response.\n    severity: warn\n    given: \"$.paths.*[get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  trustpilot-date-time-format:\n    description: Date/time fields in Trustpilot schemas must use date-time format.\n    severity: warn\n    given: \"$.components.schemas.*.properties[createdAt,updatedAt,preferredSendTime]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  trustpilot-operations-have-tags:\n    description: All Trustpilot operations should be tagged.\n    severity: warn\n    given:\
  \ \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  trustpilot-kebab-case-paths:\n    description: Trustpilot path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9]/(private/)?[a-z0-9{}-]+(/[a-z0-9{}-]+)*)+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trustpilot/refs/heads/main/rules/trustpilot-rules.yml
tags:
- Consumer Reviews
- Reviews
- Trust
- Ratings
- Business Profiles
- Product Reviews
- Spectral
- Linting
- API Governance
---
