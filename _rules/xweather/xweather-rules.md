---
api_specs:
- filename: xweather-weather-api-openapi.yml
  format: yaml
  label: Xweather Weather API
  slug: xweather
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/xweather/refs/heads/main/openapi/xweather-weather-api-openapi.yml
categories:
- xweather
description: Spectral linting rules defining API design standards and conventions for Xweather.
layout: rules
name: Xweather API Rules
provider_name: Xweather
provider_slug: xweather
rule_count: 11
rules:
- description: All Xweather API operations must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: xweather-operation-has-summary
  severity: error
- description: All Xweather API operations must be tagged.
  given: $.paths[*][get,post,put,delete,patch]
  name: xweather-operation-has-tags
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: xweather-operation-has-operation-id
  severity: error
- description: All Xweather operations must include a description explaining the data returned.
  given: $.paths[*][get,post,put,delete,patch]
  name: xweather-operation-has-description
  severity: warn
- description: All GET operations must define a 200 success response.
  given: $.paths[*].get
  name: xweather-response-200-present
  severity: error
- description: All path segments must use kebab-case.
  given: $.paths
  name: xweather-path-uses-kebab-case
  severity: warn
- description: operationId values should use camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: xweather-operation-id-camel-case
  severity: warn
- description: Tags must use Title Case.
  given: $.tags[*].name
  name: xweather-tags-title-case
  severity: warn
- description: API info must include contact information.
  given: $.info
  name: xweather-info-has-contact
  severity: warn
- description: All schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: xweather-schemas-have-descriptions
  severity: hint
- description: Success responses must define content.
  given: $.paths[*][*].responses[200,201]
  name: xweather-success-response-has-content
  severity: error
rules_file: rules/xweather-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/xweather/refs/heads/main/rules/xweather-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 6
slug: xweather-rules
source_filename: xweather-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Xweather API follows a consistent pattern of location-based paths and\n  # client_id/client_secret query parameter authentication\n  xweather-operation-has-summary:\n    description: All Xweather API operations must have a summary.\n    message: Operation must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  xweather-operation-has-tags:\n    description: All Xweather API operations must be tagged.\n    message: Operation must include at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  xweather-operation-has-operation-id:\n    description: All operations must have an operationId.\n    message: Operation must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function:\
  \ truthy\n\n  xweather-operation-has-description:\n    description: All Xweather operations must include a description explaining the data returned.\n    message: Operation must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  xweather-response-200-present:\n    description: All GET operations must define a 200 success response.\n    message: GET operations must have a 200 response defined.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: responses.200\n      function: truthy\n\n  xweather-path-uses-kebab-case:\n    description: All path segments must use kebab-case.\n    message: Path segments must use kebab-case (lowercase with hyphens, no underscores or camelCase).\n    severity: warn\n    given: $.paths\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  xweather-operation-id-camel-case:\n\
  \    description: operationId values should use camelCase.\n    message: operationId must use camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  xweather-tags-title-case:\n    description: Tags must use Title Case.\n    message: Tag names must use Title Case (e.g., \"Air Quality\" not \"air quality\").\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  xweather-info-has-contact:\n    description: API info must include contact information.\n    message: info.contact must be defined.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  xweather-schemas-have-descriptions:\n    description: All schema properties should have descriptions.\n    message: Schema properties should include a description.\n\
  \    severity: hint\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  xweather-success-response-has-content:\n    description: Success responses must define content.\n    message: 200/201 responses must include a content definition.\n    severity: error\n    given: $.paths[*][*].responses[200,201]\n    then:\n      field: content\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/xweather/refs/heads/main/rules/xweather-rules.yml
tags:
- Air Quality
- Company
- Data
- Forecasts
- Lightning
- Maritime
- Observations
- Severe Weather
- Weather
- Spectral
- Linting
- API Governance
---
