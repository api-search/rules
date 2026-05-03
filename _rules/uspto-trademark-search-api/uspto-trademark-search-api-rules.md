---
api_specs:
- filename: uspto-trademark-search-api-openapi.yml
  format: yaml
  label: USPTO Trademark Search API Endpoints
  slug: uspto-trademark-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uspto-trademark-search-api/refs/heads/main/openapi/uspto-trademark-search-api-openapi.yml
categories:
- uspto
description: Spectral linting rules defining API design standards and conventions for USPTO Trademark Search API.
layout: rules
name: USPTO Trademark Search API API Rules
provider_name: USPTO Trademark Search API
provider_slug: uspto-trademark-search-api
rule_count: 19
rules:
- description: ''
  given: $.paths[*]~
  name: uspto-trademark-path-versioned
  severity: error
- description: ''
  given: $.paths[*]~
  name: uspto-trademark-path-kebab-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-trademark-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: uspto-trademark-operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: uspto-trademark-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-trademark-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-trademark-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-trademark-tags-required
  severity: warn
- description: ''
  given: $.paths[*].get
  name: uspto-trademark-response-200-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-trademark-response-401-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uspto-trademark-parameter-description
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uspto-trademark-parameter-schema-required
  severity: error
- description: ''
  given: $.components.schemas[*].properties[*]
  name: uspto-trademark-schema-description
  severity: info
- description: ''
  given: $.components.schemas[*].properties.serialNumber
  name: uspto-trademark-serial-number-pattern
  severity: warn
- description: ''
  given: $.components.securitySchemes
  name: uspto-trademark-security-defined
  severity: error
- description: ''
  given: $
  name: uspto-trademark-global-security
  severity: warn
- description: ''
  given: $.info
  name: uspto-trademark-info-contact
  severity: warn
- description: ''
  given: $.info
  name: uspto-trademark-info-version
  severity: error
- description: ''
  given: $
  name: uspto-trademark-server-defined
  severity: error
rules_file: rules/uspto-trademark-search-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uspto-trademark-search-api/refs/heads/main/rules/uspto-trademark-search-api-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 1
  warn: 10
slug: uspto-trademark-search-api-rules
source_filename: uspto-trademark-search-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # ── Path conventions ──────────────────────────────────────────────────────────\n\n  uspto-trademark-path-versioned:\n    message: \"All paths must begin with a version prefix such as /v1/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  uspto-trademark-path-kebab-case:\n    message: \"Path segments must use kebab-case (lowercase letters, digits, hyphens, or {variables})\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9])?(/[a-z0-9-{}]+)+$\"\n\n  # ── Operation conventions ─────────────────────────────────────────────────────\n\n  uspto-trademark-operation-id-required:\n    message: \"Every operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\
  \n  uspto-trademark-operation-id-camel-case:\n    message: \"operationId must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  uspto-trademark-summary-title-case:\n    message: \"Operation summary must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  uspto-trademark-summary-required:\n    message: \"Every operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  uspto-trademark-description-required:\n    message: \"Every operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  uspto-trademark-tags-required:\n    message: \"Every operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # ── Response conventions ──────────────────────────────────────────────────────\n\n  uspto-trademark-response-200-required:\n    message: \"Every GET operation must define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  uspto-trademark-response-401-required:\n    message: \"Secured operations should document a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  # ── Parameter conventions ─────────────────────────────────────────────────────\n\n  uspto-trademark-parameter-description:\n    message: \"All parameters should have a description\"\n   \
  \ severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  uspto-trademark-parameter-schema-required:\n    message: \"All parameters must define a schema\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # ── Schema conventions ────────────────────────────────────────────────────────\n\n  uspto-trademark-schema-description:\n    message: \"Schema properties should have descriptions\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  uspto-trademark-serial-number-pattern:\n    message: \"Serial number parameters must enforce the 8-digit pattern\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.serialNumber\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n\
  \        values: [\"string\"]\n\n  # ── Security conventions ──────────────────────────────────────────────────────\n\n  uspto-trademark-security-defined:\n    message: \"API must define security schemes\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  uspto-trademark-global-security:\n    message: \"API should define global security requirements\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  # ── Info conventions ──────────────────────────────────────────────────────────\n\n  uspto-trademark-info-contact:\n    message: \"API info must include contact information\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  uspto-trademark-info-version:\n    message: \"API info must include a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  uspto-trademark-server-defined:\n\
  \    message: \"API must define at least one server\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uspto-trademark-search-api/refs/heads/main/rules/uspto-trademark-search-api-rules.yml
tags:
- Brand
- Brand Protection
- Business
- Data
- Government Data
- Intellectual Property
- Legal
- Search
- Trademark
- USPTO
- Spectral
- Linting
- API Governance
---
