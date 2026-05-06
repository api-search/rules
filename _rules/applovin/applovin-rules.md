---
api_specs:
- filename: applovin-max-revenue-reporting.yaml
  format: yaml
  label: AppLovin MAX Revenue Reporting API
  slug: applovin-max-revenue-reporting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-max-revenue-reporting.yaml
- filename: applovin-max-ad-unit-management.yaml
  format: yaml
  label: AppLovin MAX Ad Unit Management API
  slug: applovin-max-ad-unit-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-max-ad-unit-management.yaml
- filename: applovin-growth-reporting.yaml
  format: yaml
  label: AppLovin Growth (Axon / AppDiscovery) Reporting API
  slug: applovin-growth-reporting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-growth-reporting.yaml
- filename: applovin-growth-asset-reporting.yaml
  format: yaml
  label: AppLovin Growth Asset Reporting API
  slug: applovin-growth-asset-reporting
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-growth-asset-reporting.yaml
- filename: applovin-axon-campaign-management.yaml
  format: yaml
  label: AppLovin Axon Campaign Management API
  slug: applovin-axon-campaign-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-axon-campaign-management.yaml
- filename: applovin-conversion-api-lead-gen.yaml
  format: yaml
  label: AppLovin Conversion API for Lead Generation
  slug: applovin-conversion-api-lead-gen
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/openapi/applovin-conversion-api-lead-gen.yaml
categories:
- applovin
description: Spectral linting rules defining API design standards and conventions for AppLovin.
layout: rules
name: AppLovin API Rules
provider_name: AppLovin
provider_slug: applovin
rule_count: 28
rules:
- description: API title should start with "AppLovin" to match provider naming.
  given: $.info
  name: applovin-info-title-prefix
  severity: warn
- description: API spec must declare a version.
  given: $.info
  name: applovin-info-version-required
  severity: error
- description: API spec must include a non-trivial description.
  given: $.info
  name: applovin-info-description-required
  severity: warn
- description: API spec should include contact info.
  given: $.info
  name: applovin-info-contact-required
  severity: info
- description: Use OpenAPI 3.0.x.
  given: $
  name: applovin-openapi-version
  severity: error
- description: All servers must use HTTPS.
  given: $.servers[*]
  name: applovin-servers-https
  severity: error
- description: Server hosts should resolve to applovin.com or axon.ai domains.
  given: $.servers[*]
  name: applovin-servers-applovin-host
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths
  name: applovin-paths-no-trailing-slash
  severity: error
- description: AppLovin paths use snake_case segments (e.g. /ad_unit, /creative_set).
  given: $.paths
  name: applovin-paths-snake-case
  severity: warn
- description: Every operation must have a camelCase operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: applovin-operation-operationid
  severity: error
- description: Every operation must have a Title Case summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: applovin-operation-summary
  severity: error
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: applovin-operation-description
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: applovin-operation-tags
  severity: warn
- description: Operations should declare x-microcks-operation for mock dispatch.
  given: $.paths[*][get,post,put,patch,delete]
  name: applovin-operation-microcks-extension
  severity: info
- description: Tags should be declared globally with descriptions.
  given: $.tags
  name: applovin-tags-defined
  severity: warn
- description: Tag names must be Title Case.
  given: $.tags[*]
  name: applovin-tags-title-case
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][*].parameters[*]
  name: applovin-parameter-description
  severity: warn
- description: Parameter names use snake_case.
  given: $.paths[*][*].parameters[?(@.in=='query' || @.in=='path')]
  name: applovin-parameter-snake-case
  severity: warn
- description: Every parameter must declare a schema with a type.
  given: $.paths[*][*].parameters[*].schema
  name: applovin-parameter-schema-type
  severity: error
- description: Every operation must define a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: applovin-response-success
  severity: error
- description: Authenticated operations should declare 401.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: applovin-response-unauthorized
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][*].responses[*]
  name: applovin-response-description
  severity: warn
- description: Schema property names must be snake_case.
  given: $.components.schemas[*].properties
  name: applovin-schema-snake-case-property
  severity: warn
- description: Every schema property must have a type or $ref.
  given: $.components.schemas[*].properties[*]
  name: applovin-schema-property-type
  severity: error
- description: Security schemes must be defined.
  given: $
  name: applovin-security-defined
  severity: error
- description: Top-level security must be defined.
  given: $
  name: applovin-security-global
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: applovin-get-no-body
  severity: error
- description: POST operations should have a request body.
  given: $.paths[*].post
  name: applovin-post-body
  severity: warn
rules_file: rules/applovin-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/rules/applovin-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 2
  warn: 15
slug: applovin-rules
source_filename: applovin-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\ndocumentationUrl: https://github.com/api-evangelist/applovin\n\n# Spectral ruleset for AppLovin / Axon REST APIs\n# Derived from OpenAPI specs in openapi/ — enforces patterns\n# observed across MAX, Growth, Axon Campaign Management, and CAPI APIs.\n\nrules:\n  # ---------------- INFO / METADATA ----------------\n  applovin-info-title-prefix:\n    description: API title should start with \"AppLovin\" to match provider naming.\n    message: 'info.title should start with \"AppLovin\"'\n    severity: warn\n    given: $.info\n    then:\n      field: title\n      function: pattern\n      functionOptions:\n        match: '^AppLovin'\n\n  applovin-info-version-required:\n    description: API spec must declare a version.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  applovin-info-description-required:\n    description: API spec must include a non-trivial description.\n    severity: warn\n    given:\
  \ $.info\n    then:\n      field: description\n      function: length\n      functionOptions:\n        min: 80\n\n  applovin-info-contact-required:\n    description: API spec should include contact info.\n    severity: info\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # ---------------- OPENAPI VERSION ----------------\n  applovin-openapi-version:\n    description: Use OpenAPI 3.0.x.\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: '^3\\.0\\.'\n\n  # ---------------- SERVERS ----------------\n  applovin-servers-https:\n    description: All servers must use HTTPS.\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: '^https://'\n\n  applovin-servers-applovin-host:\n    description: Server hosts should resolve to applovin.com or axon.ai domains.\n    severity: warn\n    given: $.servers[*]\n\
  \    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: '(applovin\\.com|axon\\.ai)'\n\n  # ---------------- PATHS ----------------\n  applovin-paths-no-trailing-slash:\n    description: Paths must not have a trailing slash.\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      field: '@key'\n      functionOptions:\n        notMatch: '.+/$'\n\n  applovin-paths-snake-case:\n    description: AppLovin paths use snake_case segments (e.g. /ad_unit, /creative_set).\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      field: '@key'\n      functionOptions:\n        match: '^(/[a-z0-9_]+(\\{[a-z_]+\\})?)+$'\n\n  # ---------------- OPERATIONS ----------------\n  applovin-operation-operationid:\n    description: Every operation must have a camelCase operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: pattern\n     \
  \ functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  applovin-operation-summary:\n    description: Every operation must have a Title Case summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  applovin-operation-description:\n    description: Every operation must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  applovin-operation-tags:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  applovin-operation-microcks-extension:\n    description: Operations should declare x-microcks-operation for mock dispatch.\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n\
  \      function: truthy\n\n  # ---------------- TAGS ----------------\n  applovin-tags-defined:\n    description: Tags should be declared globally with descriptions.\n    severity: warn\n    given: $.tags\n    then:\n      function: truthy\n\n  applovin-tags-title-case:\n    description: Tag names must be Title Case.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z0-9]*( [A-Z][A-Za-z0-9]*)*$'\n\n  # ---------------- PARAMETERS ----------------\n  applovin-parameter-description:\n    description: Every parameter must have a description.\n    severity: warn\n    given: $.paths[*][*].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  applovin-parameter-snake-case:\n    description: Parameter names use snake_case.\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.in=='query' || @.in=='path')]\n    then:\n      field: name\n      function: pattern\n\
  \      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  applovin-parameter-schema-type:\n    description: Every parameter must declare a schema with a type.\n    severity: error\n    given: $.paths[*][*].parameters[*].schema\n    then:\n      field: type\n      function: truthy\n\n  # ---------------- RESPONSES ----------------\n  applovin-response-success:\n    description: Every operation must define a 2xx response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: pattern\n      field: '@key'\n      functionOptions:\n        match: '^(2[0-9][0-9])$'\n\n  applovin-response-unauthorized:\n    description: Authenticated operations should declare 401.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '401'\n      function: truthy\n\n  applovin-response-description:\n    description: Every response must have a description.\n    severity: warn\n    given: $.paths[*][*].responses[*]\n\
  \    then:\n      field: description\n      function: truthy\n\n  # ---------------- SCHEMAS ----------------\n  applovin-schema-snake-case-property:\n    description: Schema property names must be snake_case.\n    severity: warn\n    given: $.components.schemas[*].properties\n    then:\n      function: pattern\n      field: '@key'\n      functionOptions:\n        match: '^[a-z][a-z0-9_]*$'\n\n  applovin-schema-property-type:\n    description: Every schema property must have a type or $ref.\n    severity: error\n    given: $.components.schemas[*].properties[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [type]\n            - required: ['$ref']\n            - required: [oneOf]\n            - required: [allOf]\n            - required: [anyOf]\n\n  # ---------------- SECURITY ----------------\n  applovin-security-defined:\n    description: Security schemes must be defined.\n    severity: error\n    given: $\n    then:\n\
  \      field: components.securitySchemes\n      function: truthy\n\n  applovin-security-global:\n    description: Top-level security must be defined.\n    severity: warn\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  # ---------------- HTTP METHOD CONVENTIONS ----------------\n  applovin-get-no-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  applovin-post-body:\n    description: POST operations should have a request body.\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/applovin/refs/heads/main/rules/applovin-rules.yml
tags:
- Advertising
- Mobile
- AdTech
- App Monetization
- Mediation
- User Acquisition
- Marketing Technology
- Conversion Tracking
- Spectral
- Linting
- API Governance
---
