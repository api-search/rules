---
api_specs:
- filename: fred-openapi.yml
  format: yaml
  label: FRED API - Reserve Data
  slug: fred-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reserve-requirements/refs/heads/main/openapi/fred-openapi.yml
categories:
- fred
description: Spectral linting rules defining API design standards and conventions for Reserve Requirements.
layout: rules
name: Reserve Requirements API Rules
provider_name: Reserve Requirements
provider_slug: reserve-requirements
rule_count: 10
rules:
- description: All FRED API operations must include the api_key parameter.
  given: $.paths[*][get,post]
  name: fred-api-key-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: fred-operation-id
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: fred-operation-summary
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: fred-operation-tags
  severity: warn
- description: All FRED operations should support file_type parameter.
  given: $.paths[*][get]
  name: fred-file-type-param
  severity: info
- description: All GET operations should have a 200 success response.
  given: $.paths[*].get
  name: fred-response-200
  severity: error
- description: Success responses should reference a schema.
  given: $.paths[*].get.responses['200'].content
  name: fred-response-schema
  severity: warn
- description: All responses should support application/json.
  given: $.paths[*][*].responses['200'].content
  name: fred-json-content-type
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: fred-tags-title-case
  severity: warn
- description: series_id parameters should have descriptions with example FRED series IDs.
  given: $.paths[*][*].parameters[?(@.name == 'series_id')]
  name: fred-series-id-described
  severity: info
rules_file: rules/reserve-requirements-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reserve-requirements/refs/heads/main/rules/reserve-requirements-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 4
slug: reserve-requirements-rules
source_filename: reserve-requirements-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  fred-api-key-required:\n    description: All FRED API operations must include the api_key parameter.\n    message: Operation should document the api_key query parameter.\n    severity: error\n    given: $.paths[*][get,post]\n    then:\n      field: parameters\n      function: truthy\n\n  fred-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  fred-operation-summary:\n    description: All operations must have a summary.\n    message: Operation is missing a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  fred-operation-tags:\n    description: All operations must have at least one tag.\n    message: Operation is missing tags.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n\
  \    then:\n      field: tags\n      function: truthy\n\n  fred-file-type-param:\n    description: All FRED operations should support file_type parameter.\n    message: Operation should document file_type query parameter.\n    severity: info\n    given: $.paths[*][get]\n    then:\n      field: parameters\n      function: truthy\n\n  fred-response-200:\n    description: All GET operations should have a 200 success response.\n    message: GET operation should have a 200 response.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: responses.200\n      function: truthy\n\n  fred-response-schema:\n    description: Success responses should reference a schema.\n    message: 200 response should include a content schema.\n    severity: warn\n    given: $.paths[*].get.responses['200'].content\n    then:\n      function: truthy\n\n  fred-json-content-type:\n    description: All responses should support application/json.\n    message: Response should include application/json\
  \ content type.\n    severity: warn\n    given: $.paths[*][*].responses['200'].content\n    then:\n      field: application/json\n      function: truthy\n\n  fred-tags-title-case:\n    description: All tags must use Title Case.\n    message: Tag name should use Title Case.\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z ]*$'\n\n  fred-series-id-described:\n    description: series_id parameters should have descriptions with example FRED series IDs.\n    message: series_id parameter should be well described.\n    severity: info\n    given: $.paths[*][*].parameters[?(@.name == 'series_id')]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reserve-requirements/refs/heads/main/rules/reserve-requirements-rules.yml
tags:
- Reserve Requirements
- Federal Reserve
- Banking Regulation
- Monetary Policy
- Regulation D
- Finance
- Spectral
- Linting
- API Governance
---
