---
api_specs:
- filename: uspto-patent-api-openapi.yml
  format: yaml
  label: USPTO Patent & Trademark API
  slug: patent-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uspto/refs/heads/main/openapi/uspto-patent-api-openapi.yml
- filename: index.html
  format: yaml
  label: USPTO Patent Trial and Appeal Board (PTAB) API
  slug: ptab-api
  spec_type: OpenAPI
  url: https://data.uspto.gov/swagger/index.html
- filename: tsdr-api-v1
  format: yaml
  label: USPTO Trademark Status and Document Retrieval (TSDR) API
  slug: tsdr-api
  spec_type: OpenAPI
  url: https://developer.uspto.gov/swagger/tsdr-api-v1
- filename: oa_actions.json
  format: json
  label: USPTO Office Action Text Retrieval API
  slug: office-actions-api
  spec_type: OpenAPI
  url: https://developer.uspto.gov/ds-api/swagger/docs/oa_actions.json
- filename: enriched_cited_reference_metadata.json
  format: json
  label: USPTO Enriched Citation API
  slug: enriched-citation-api
  spec_type: OpenAPI
  url: https://developer.uspto.gov/ds-api/swagger/docs/enriched_cited_reference_metadata.json
categories:
- uspto
description: Spectral linting rules defining API design standards and conventions for USPTO.
layout: rules
name: USPTO API Rules
provider_name: USPTO
provider_slug: uspto
rule_count: 20
rules:
- description: ''
  given: $.paths[*]~
  name: uspto-path-versioned
  severity: error
- description: ''
  given: $.paths[*]~
  name: uspto-path-kebab-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: uspto-operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: uspto-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-tags-required
  severity: warn
- description: ''
  given: $.paths[*].get
  name: uspto-response-200-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: uspto-response-401-recommended
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: uspto-response-404-recommended
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uspto-parameter-description
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uspto-parameter-schema-required
  severity: error
- description: ''
  given: $.components.schemas[*]
  name: uspto-schema-description
  severity: info
- description: ''
  given: $.components.schemas[*].properties.status
  name: uspto-enum-upper-case
  severity: info
- description: ''
  given: $.components.securitySchemes
  name: uspto-security-defined
  severity: error
- description: ''
  given: $
  name: uspto-global-security
  severity: warn
- description: ''
  given: $.info
  name: uspto-info-contact
  severity: warn
- description: ''
  given: $.info
  name: uspto-info-license
  severity: error
- description: ''
  given: $
  name: uspto-server-defined
  severity: error
rules_file: rules/uspto-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uspto/refs/heads/main/rules/uspto-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 3
  warn: 9
slug: uspto-rules
source_filename: uspto-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # ── Path conventions ──────────────────────────────────────────────────────────\n\n  uspto-path-versioned:\n    message: \"All paths must begin with a version prefix such as /v1/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z]\"\n\n  uspto-path-kebab-case:\n    message: \"Path segments must use kebab-case (lowercase, digits, hyphens, or {variables})\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}]+)+$\"\n\n  # ── Operation conventions ─────────────────────────────────────────────────────\n\n  uspto-operation-id-required:\n    message: \"Every operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  uspto-operation-id-camel-case:\n    message:\
  \ \"operationId must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  uspto-summary-required:\n    message: \"Every operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  uspto-summary-title-case:\n    message: \"Operation summary must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  uspto-description-required:\n    message: \"Every operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  uspto-tags-required:\n    message: \"Every operation must have at least one\
  \ tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # ── Response conventions ──────────────────────────────────────────────────────\n\n  uspto-response-200-required:\n    message: \"GET operations must define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  uspto-response-401-recommended:\n    message: \"Secured operations should document 401 Unauthorized\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  uspto-response-404-recommended:\n    message: \"Operations with path parameters should document 404 Not Found\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # ── Parameter conventions\
  \ ─────────────────────────────────────────────────────\n\n  uspto-parameter-description:\n    message: \"All parameters should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  uspto-parameter-schema-required:\n    message: \"All parameters must define a schema\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # ── Schema conventions ────────────────────────────────────────────────────────\n\n  uspto-schema-description:\n    message: \"Schema component descriptions are recommended\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  uspto-enum-upper-case:\n    message: \"Enum values representing status codes should use UPPER_CASE\"\n    severity: info\n    given: \"$.components.schemas[*].properties.status\"\
  \n    then:\n      field: enum\n      function: truthy\n\n  # ── Security conventions ──────────────────────────────────────────────────────\n\n  uspto-security-defined:\n    message: \"API must define security schemes\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  uspto-global-security:\n    message: \"API should define global security requirements\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  # ── Info conventions ──────────────────────────────────────────────────────────\n\n  uspto-info-contact:\n    message: \"API info must include contact information\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  uspto-info-license:\n    message: \"Government APIs must include a license statement\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  uspto-server-defined:\n\
  \    message: \"API must define at least one server\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uspto/refs/heads/main/rules/uspto-rules.yml
tags:
- Government
- Intellectual Property
- Open Data
- Patents
- Regulatory
- Trademarks
- USPTO
- Spectral
- Linting
- API Governance
---
