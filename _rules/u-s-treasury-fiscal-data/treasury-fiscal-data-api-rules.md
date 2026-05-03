---
api_specs:
- filename: treasury-fiscal-data-api-openapi.yaml
  format: yaml
  label: Treasury Fiscal Data API
  slug: fiscal-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/u-s-treasury-fiscal-data/refs/heads/main/openapi/treasury-fiscal-data-api-openapi.yaml
categories:
- treasury
description: Spectral linting rules defining API design standards and conventions for U.S. Treasury Fiscal Data.
layout: rules
name: U.S. Treasury Fiscal Data API Rules
provider_name: U.S. Treasury Fiscal Data
provider_slug: u-s-treasury-fiscal-data
rule_count: 31
rules:
- description: API must have a title in the info object.
  given: $.info
  name: treasury-info-title-present
  severity: error
- description: API must have a description in the info object.
  given: $.info
  name: treasury-info-description-present
  severity: warn
- description: API must have a version in the info object.
  given: $.info
  name: treasury-info-version-present
  severity: error
- description: API info should include contact information.
  given: $.info
  name: treasury-info-contact-present
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: treasury-operation-id-present
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: treasury-operation-summary-present
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: treasury-operation-description-present
  severity: info
- description: All operations should have tags.
  given: $.paths[*][get,post,put,patch,delete]
  name: treasury-operation-tags-present
  severity: warn
- description: OperationId should use camelCase naming convention.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: treasury-operation-id-pascal-case
  severity: warn
- description: All parameters should have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: treasury-parameter-description-present
  severity: warn
- description: Query parameters should follow Treasury API naming conventions.
  given: $.paths[*].get.parameters[?(@.in=="query")].name
  name: treasury-query-parameter-style
  severity: info
- description: All GET operations must have a 200 response.
  given: $.paths[*].get
  name: treasury-response-200-present
  severity: error
- description: Operations should define a 400 error response.
  given: $.paths[*][get,post,put,patch,delete]
  name: treasury-response-400-present
  severity: warn
- description: All responses should have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: treasury-response-description-present
  severity: warn
- description: Successful responses should reference a schema.
  given: $.paths[*][get,post].responses['200'].content['application/json']
  name: treasury-response-schema-present
  severity: warn
- description: All schemas in components should have a description.
  given: $.components.schemas[*]
  name: treasury-schema-description-present
  severity: info
- description: Object schemas should define properties.
  given: $.components.schemas[?(@.type=="object")]
  name: treasury-schema-properties-present
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: treasury-property-description-present
  severity: info
- description: Schema properties should declare a type.
  given: $.components.schemas[*].properties[*]
  name: treasury-property-type-present
  severity: warn
- description: Treasury fiscal endpoints should support fields parameter for field selection.
  given: $.paths[*].get.parameters
  name: treasury-pagination-fields-param
  severity: info
- description: Treasury fiscal endpoints should support filter parameter for data filtering.
  given: $.paths[*].get.parameters
  name: treasury-pagination-filter-param
  severity: info
- description: Successful responses should use the standard data envelope with meta and links.
  given: $.components.schemas[?(@.properties.data && @.properties.meta && @.properties.links)]
  name: treasury-response-data-envelope
  severity: info
- description: All tags used in operations must be defined at the top level.
  given: $.tags
  name: treasury-tags-defined
  severity: warn
- description: All top-level tags should have descriptions.
  given: $.tags[*]
  name: treasury-tag-description-present
  severity: info
- description: API must define at least one server.
  given: $
  name: treasury-servers-present
  severity: error
- description: Server URLs should use HTTPS.
  given: $.servers[*].url
  name: treasury-server-url-https
  severity: error
- description: Servers should have descriptions.
  given: $.servers[*]
  name: treasury-server-description-present
  severity: info
- description: API should define reusable schemas in components.
  given: $.components
  name: treasury-components-schemas-present
  severity: info
- description: API should define reusable parameters in components.
  given: $.components
  name: treasury-components-parameters-present
  severity: info
- description: Treasury Fiscal Data API paths should include a version prefix (v1, v2, etc.).
  given: $.paths[*]~
  name: treasury-path-version-prefix
  severity: warn
- description: Path segments should be lowercase with underscores.
  given: $.paths[*]~
  name: treasury-path-lowercase
  severity: info
rules_file: rules/treasury-fiscal-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/u-s-treasury-fiscal-data/refs/heads/main/rules/treasury-fiscal-data-api-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 12
  warn: 13
slug: treasury-fiscal-data-api-rules
source_filename: treasury-fiscal-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\nrules:\n\n  # ─── Info ───────────────────────────────────────────────────────────────────\n  treasury-info-title-present:\n    description: API must have a title in the info object.\n    message: \"{{description}}\"\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  treasury-info-description-present:\n    description: API must have a description in the info object.\n    message: \"{{description}}\"\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  treasury-info-version-present:\n    description: API must have a version in the info object.\n    message: \"{{description}}\"\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  treasury-info-contact-present:\n    description: API info should include contact information.\n    message: \"{{description}}\"\n    severity: warn\n    given: $.info\n\
  \    then:\n      field: contact\n      function: truthy\n\n  # ─── Operations ─────────────────────────────────────────────────────────────\n  treasury-operation-id-present:\n    description: All operations must have an operationId.\n    message: \"Operation missing operationId: {{path}}\"\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  treasury-operation-summary-present:\n    description: All operations must have a summary.\n    message: \"Operation missing summary: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  treasury-operation-description-present:\n    description: All operations should have a description.\n    message: \"Operation missing description: {{path}}\"\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  treasury-operation-tags-present:\n\
  \    description: All operations should have tags.\n    message: \"Operation missing tags: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  treasury-operation-id-pascal-case:\n    description: OperationId should use camelCase naming convention.\n    message: \"OperationId '{{value}}' should be camelCase: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # ─── Parameters ─────────────────────────────────────────────────────────────\n  treasury-parameter-description-present:\n    description: All parameters should have a description.\n    message: \"Parameter '{{value}}' missing description: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  treasury-query-parameter-style:\n\
  \    description: Query parameters should follow Treasury API naming conventions.\n    message: \"Query parameter '{{value}}' should use snake_case or dot notation: {{path}}\"\n    severity: info\n    given: $.paths[*].get.parameters[?(@.in==\"query\")].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9_\\\\[\\\\]]+$\"\n\n  # ─── Responses ──────────────────────────────────────────────────────────────\n  treasury-response-200-present:\n    description: All GET operations must have a 200 response.\n    message: \"GET operation missing 200 response: {{path}}\"\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: responses.200\n      function: truthy\n\n  treasury-response-400-present:\n    description: Operations should define a 400 error response.\n    message: \"Operation missing 400 response: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses.400\n    \
  \  function: truthy\n\n  treasury-response-description-present:\n    description: All responses should have a description.\n    message: \"Response missing description: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  treasury-response-schema-present:\n    description: Successful responses should reference a schema.\n    message: \"Response missing content/schema: {{path}}\"\n    severity: warn\n    given: $.paths[*][get,post].responses['200'].content['application/json']\n    then:\n      field: schema\n      function: truthy\n\n  # ─── Schemas ────────────────────────────────────────────────────────────────\n  treasury-schema-description-present:\n    description: All schemas in components should have a description.\n    message: \"Schema '{{path}}' missing description.\"\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function:\
  \ truthy\n\n  treasury-schema-properties-present:\n    description: Object schemas should define properties.\n    message: \"Object schema missing properties: {{path}}\"\n    severity: warn\n    given: $.components.schemas[?(@.type==\"object\")]\n    then:\n      field: properties\n      function: truthy\n\n  treasury-property-description-present:\n    description: Schema properties should have descriptions.\n    message: \"Property missing description: {{path}}\"\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: truthy\n\n  treasury-property-type-present:\n    description: Schema properties should declare a type.\n    message: \"Property missing type: {{path}}\"\n    severity: warn\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: type\n      function: truthy\n\n  # ─── Fiscal Data Conventions ─────────────────────────────────────────────────\n  treasury-pagination-fields-param:\n    description:\
  \ Treasury fiscal endpoints should support fields parameter for field selection.\n    message: \"Fiscal endpoint missing 'fields' parameter support: {{path}}\"\n    severity: info\n    given: $.paths[*].get.parameters\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              $ref:\n                type: string\n                pattern: \"fields\"\n            required: [\"$ref\"]\n\n  treasury-pagination-filter-param:\n    description: Treasury fiscal endpoints should support filter parameter for data filtering.\n    message: \"Fiscal endpoint missing 'filter' parameter support: {{path}}\"\n    severity: info\n    given: $.paths[*].get.parameters\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              $ref:\n                type: string\n\
  \                pattern: \"filter\"\n            required: [\"$ref\"]\n\n  treasury-response-data-envelope:\n    description: Successful responses should use the standard data envelope with meta and links.\n    message: \"Response schema should include data, meta, and links properties: {{path}}\"\n    severity: info\n    given: $.components.schemas[?(@.properties.data && @.properties.meta && @.properties.links)]\n    then:\n      function: truthy\n\n  # ─── Tags ────────────────────────────────────────────────────────────────────\n  treasury-tags-defined:\n    description: All tags used in operations must be defined at the top level.\n    message: \"Tag used but not defined in tags object: {{path}}\"\n    severity: warn\n    given: $.tags\n    then:\n      field: name\n      function: truthy\n\n  treasury-tag-description-present:\n    description: All top-level tags should have descriptions.\n    message: \"Tag missing description: {{path}}\"\n    severity: info\n    given: $.tags[*]\n\
  \    then:\n      field: description\n      function: truthy\n\n  # ─── Servers ────────────────────────────────────────────────────────────────\n  treasury-servers-present:\n    description: API must define at least one server.\n    message: \"{{description}}\"\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  treasury-server-url-https:\n    description: Server URLs should use HTTPS.\n    message: \"Server URL should use HTTPS: {{value}}\"\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  treasury-server-description-present:\n    description: Servers should have descriptions.\n    message: \"Server missing description: {{path}}\"\n    severity: info\n    given: $.servers[*]\n    then:\n      field: description\n      function: truthy\n\n  # ─── Components ─────────────────────────────────────────────────────────────\n  treasury-components-schemas-present:\n\
  \    description: API should define reusable schemas in components.\n    message: \"{{description}}\"\n    severity: info\n    given: $.components\n    then:\n      field: schemas\n      function: truthy\n\n  treasury-components-parameters-present:\n    description: API should define reusable parameters in components.\n    message: \"{{description}}\"\n    severity: info\n    given: $.components\n    then:\n      field: parameters\n      function: truthy\n\n  # ─── Paths ──────────────────────────────────────────────────────────────────\n  treasury-path-version-prefix:\n    description: Treasury Fiscal Data API paths should include a version prefix (v1, v2, etc.).\n    message: \"Path should include version prefix like /v1/ or /v2/: {{path}}\"\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]/\"\n\n  treasury-path-lowercase:\n    description: Path segments should be lowercase with underscores.\n    message:\
  \ \"Path should use lowercase with underscores: {{path}}\"\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9_{}-]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/u-s-treasury-fiscal-data/refs/heads/main/rules/treasury-fiscal-data-api-rules.yml
tags:
- Federal Government
- Finance
- Treasury
- National Debt
- Exchange Rates
- Economics
- Spectral
- Linting
- API Governance
---
