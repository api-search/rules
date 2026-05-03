---
api_specs:
- filename: shopper-approved-openapi.yml
  format: yaml
  label: Shopper Approved API
  slug: shopper-approved-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopper-approved/refs/heads/main/openapi/shopper-approved-openapi.yml
categories:
- shopper
description: Spectral linting rules defining API design standards and conventions for Shopper Approved.
layout: rules
name: Shopper Approved API Rules
provider_name: Shopper Approved
provider_slug: shopper-approved
rule_count: 7
rules:
- description: Shopper Approved API uses site_id as a path parameter in all endpoints
  given: $.paths[*]~
  name: shopper-approved-site-id-path
  severity: warn
- description: Shopper Approved API requires token as a query parameter
  given: $.paths[*][get,post,put].parameters[?(@.in == 'query' && @.name == 'token')]
  name: shopper-approved-token-query-param
  severity: warn
- description: All Shopper Approved API operations must have operationIds
  given: $.paths[*][get,post,put,delete,patch]
  name: shopper-approved-operation-ids
  severity: error
- description: All operations must be tagged for grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: shopper-approved-tag-required
  severity: warn
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: shopper-approved-response-200
  severity: error
- description: Review rating should be constrained to 1-5 range
  given: $.components.schemas.Review.properties.rating
  name: shopper-approved-rating-schema
  severity: warn
- description: Shopper Approved API should use HTTPS
  given: $.servers[*].url
  name: shopper-approved-https-server
  severity: error
rules_file: rules/shopper-approved-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shopper-approved/refs/heads/main/rules/shopper-approved-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: shopper-approved-rules
source_filename: shopper-approved-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shopper-approved-site-id-path:\n    description: Shopper Approved API uses site_id as a path parameter in all endpoints\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{site_id\\\\}\"\n\n  shopper-approved-token-query-param:\n    description: Shopper Approved API requires token as a query parameter\n    severity: warn\n    given: \"$.paths[*][get,post,put].parameters[?(@.in == 'query' && @.name == 'token')]\"\n    then:\n      field: required\n      function: truthy\n\n  shopper-approved-operation-ids:\n    description: All Shopper Approved API operations must have operationIds\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  shopper-approved-tag-required:\n    description: All operations must be tagged for grouping\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  shopper-approved-response-200:\n    description: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  shopper-approved-rating-schema:\n    description: Review rating should be constrained to 1-5 range\n    severity: warn\n    given: \"$.components.schemas.Review.properties.rating\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - minimum\n            - maximum\n\n  shopper-approved-https-server:\n    description: Shopper Approved API should use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shopper-approved/refs/heads/main/rules/shopper-approved-rules.yml
tags:
- Reviews
- Ratings
- Ecommerce
- Customer Feedback
- Social Proof
- Spectral
- Linting
- API Governance
---
