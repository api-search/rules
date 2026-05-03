---
api_specs:
- filename: trefle-openapi.yml
  format: yaml
  label: Trefle API
  slug: trefle
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trefle/refs/heads/main/openapi/trefle-openapi.yml
categories:
- trefle
description: Spectral linting rules defining API design standards and conventions for Trefle.
layout: rules
name: Trefle API Rules
provider_name: Trefle
provider_slug: trefle
rule_count: 9
rules:
- description: All Trefle API operations should have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: trefle-operation-id-required
  severity: error
- description: The Trefle API uses token-based authentication. The global security scheme should specify the tokenAuth apiKey scheme.
  given: $
  name: trefle-token-auth-documented
  severity: warn
- description: All Trefle API GET operations should define a 200 response.
  given: $.paths[*].get.responses
  name: trefle-response-200-defined
  severity: error
- description: All operations should document 401 Unauthorized for token auth errors.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: trefle-response-401-defined
  severity: warn
- description: Endpoints with path parameters (individual resource lookups) should document the 404 Not Found response.
  given: $.paths[*{id}*][get].responses
  name: trefle-response-404-on-id-paths
  severity: warn
- description: All operations should have at least one tag for navigation.
  given: $.paths[*][*].tags
  name: trefle-tags-required
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][*]
  name: trefle-description-required
  severity: warn
- description: All operations should have a summary.
  given: $.paths[*][*]
  name: trefle-summary-required
  severity: error
- description: List operations (returning arrays) should include pagination links in the 200 response, consistent with the Trefle API data/links/meta structure.
  given: $.paths[*].get.responses.200
  name: trefle-pagination-links
  severity: info
rules_file: rules/trefle-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trefle/refs/heads/main/rules/trefle-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: trefle-rules
source_filename: trefle-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trefle-operation-id-required:\n    description: All Trefle API operations should have an operationId.\n    message: \"Operation should have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  trefle-token-auth-documented:\n    description: >-\n      The Trefle API uses token-based authentication. The global security\n      scheme should specify the tokenAuth apiKey scheme.\n    message: \"API should declare global security with token authentication\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  trefle-response-200-defined:\n    description: All Trefle API GET operations should define a 200 response.\n    message: \"GET operation should define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      function: schema\n      functionOptions:\n  \
  \      schema:\n          required: [\"200\"]\n\n  trefle-response-401-defined:\n    description: All operations should document 401 Unauthorized for token auth errors.\n    message: \"Operation should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  trefle-response-404-on-id-paths:\n    description: >-\n      Endpoints with path parameters (individual resource lookups) should\n      document the 404 Not Found response.\n    message: \"ID-based lookup should define a 404 Not Found response\"\n    severity: warn\n    given: \"$.paths[*{id}*][get].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"404\"]\n\n  trefle-tags-required:\n    description: All operations should have at least one tag for navigation.\n    message: \"Operation should have at\
  \ least one tag\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  trefle-description-required:\n    description: All operations should have a description.\n    message: \"Operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  trefle-summary-required:\n    description: All operations should have a summary.\n    message: \"Operation should have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  trefle-pagination-links:\n    description: >-\n      List operations (returning arrays) should include pagination links in\n      the 200 response, consistent with the Trefle API data/links/meta structure.\n    message: \"List operation should include pagination links in response schema\"\n    severity: info\n    given: \"$.paths[*].get.responses.200\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trefle/refs/heads/main/rules/trefle-rules.yml
tags:
- Agriculture
- Botany
- Open Data
- Plants
- Science
- Spectral
- Linting
- API Governance
---
