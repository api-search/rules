---
api_specs:
- filename: solcast-openapi.yml
  format: yaml
  label: Solcast API
  slug: solcast
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/solcast/refs/heads/main/openapi/solcast-openapi.yml
categories:
- solcast
description: Spectral linting rules defining API design standards and conventions for Solcast.
layout: rules
name: Solcast API Rules
provider_name: Solcast
provider_slug: solcast
rule_count: 18
rules:
- description: API info object must include a contact with a URL.
  given: $.info.contact
  name: solcast-info-contact
  severity: warn
- description: API info must have a version field.
  given: $.info
  name: solcast-info-version
  severity: error
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: solcast-operation-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][*]
  name: solcast-operation-has-tags
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][*]
  name: solcast-operation-has-description
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][*]
  name: solcast-operation-has-operationid
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][*].operationId
  name: solcast-operationid-camel-case
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][*].parameters[*]
  name: solcast-parameter-has-description
  severity: warn
- description: Latitude query parameter must specify minimum/maximum range constraints.
  given: $.paths[*][*].parameters[?(@.name == 'latitude')]
  name: solcast-lat-lon-parameter-range
  severity: warn
- description: Format query parameters must restrict to valid values using enum.
  given: $.paths[*][*].parameters[?(@.name == 'format')]
  name: solcast-format-parameter-enum
  severity: warn
- description: Every GET operation must define a 200 response.
  given: $.paths[*].get
  name: solcast-response-200-defined
  severity: error
- description: Every operation must define a 401 Unauthorized response.
  given: $.paths[*][*]
  name: solcast-response-401-defined
  severity: warn
- description: Every operation must define a 429 Too Many Requests response.
  given: $.paths[*][*]
  name: solcast-response-429-defined
  severity: warn
- description: All schema properties must have descriptions.
  given: $.components.schemas[*].properties[*]
  name: solcast-schema-properties-described
  severity: warn
- description: Schema objects must not be empty (must have properties or $ref).
  given: $.components.schemas[*]
  name: solcast-no-empty-schemas
  severity: error
- description: API paths must use kebab-case or snake_case segments consistently.
  given: $.paths[*]~
  name: solcast-path-kebab-case
  severity: warn
- description: API must define global security (Bearer token required).
  given: $
  name: solcast-global-security-defined
  severity: error
- description: The security scheme must be a Bearer token scheme.
  given: $.components.securitySchemes[*]
  name: solcast-security-scheme-bearer
  severity: error
rules_file: rules/solcast-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/solcast/refs/heads/main/rules/solcast-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 12
slug: solcast-rules
source_filename: solcast-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # ─── Info Object Rules ────────────────────────────────────────────────────\n  solcast-info-contact:\n    description: API info object must include a contact with a URL.\n    message: \"Info contact must have a url field pointing to Solcast support.\"\n    severity: warn\n    given: \"$.info.contact\"\n    then:\n      field: url\n      function: truthy\n\n  solcast-info-version:\n    description: API info must have a version field.\n    message: \"Info object must specify a version string.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # ─── Operation Rules ──────────────────────────────────────────────────────\n  solcast-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^([A-Z][a-z0-9]*)( [A-Z][a-z0-9]*)*$\"\n\n  solcast-operation-has-tags:\n    description: Every operation must have at least one tag.\n    message: \"Operation '{{path}}' must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  solcast-operation-has-description:\n    description: Every operation must have a description.\n    message: \"Operation '{{path}}' must have a description.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  solcast-operation-has-operationid:\n    description: Every operation must have an operationId.\n    message: \"Operation at '{{path}}' is missing an operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  solcast-operationid-camel-case:\n    description: operationId must use camelCase.\n    message:\
  \ \"operationId '{{value}}' must use camelCase (e.g., getLiveRadiationAndWeather).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ─── Parameter Rules ──────────────────────────────────────────────────────\n  solcast-parameter-has-description:\n    description: All parameters must have a description.\n    message: \"Parameter '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  solcast-lat-lon-parameter-range:\n    description: Latitude query parameter must specify minimum/maximum range constraints.\n    message: \"Latitude parameter '{{path}}' must declare minimum: -90 and maximum: 90.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'latitude')]\"\n    then:\n      field: schema.minimum\n      function: defined\n\n  solcast-format-parameter-enum:\n\
  \    description: Format query parameters must restrict to valid values using enum.\n    message: \"The 'format' parameter must use an enum restricting values to json and csv.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'format')]\"\n    then:\n      field: schema.enum\n      function: truthy\n\n  # ─── Response Rules ───────────────────────────────────────────────────────\n  solcast-response-200-defined:\n    description: Every GET operation must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  solcast-response-401-defined:\n    description: Every operation must define a 401 Unauthorized response.\n    message: \"Operation '{{path}}' must define a 401 response (API key required).\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.401\n      function: truthy\n\
  \n  solcast-response-429-defined:\n    description: Every operation must define a 429 Too Many Requests response.\n    message: \"Operation '{{path}}' must define a 429 response (rate limiting enforced).\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.429\n      function: truthy\n\n  # ─── Schema Rules ─────────────────────────────────────────────────────────\n  solcast-schema-properties-described:\n    description: All schema properties must have descriptions.\n    message: \"Schema property '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  solcast-no-empty-schemas:\n    description: Schema objects must not be empty (must have properties or $ref).\n    message: \"Schema '{{path}}' appears to be empty — add properties or a $ref.\"\n    severity: error\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          anyOf:\n            - required: [properties]\n            - required: [$ref]\n            - required: [allOf]\n            - required: [oneOf]\n            - required: [anyOf]\n\n  # ─── Path Rules ───────────────────────────────────────────────────────────\n  solcast-path-kebab-case:\n    description: API paths must use kebab-case or snake_case segments consistently.\n    message: \"Path '{{path}}' must use lowercase path segments.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9/_{}.-]+$\"\n\n  # ─── Security Rules ───────────────────────────────────────────────────────\n  solcast-global-security-defined:\n    description: API must define global security (Bearer token required).\n    message: \"The API must define a global security requirement for Bearer token auth.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n   \
  \   function: truthy\n\n  solcast-security-scheme-bearer:\n    description: The security scheme must be a Bearer token scheme.\n    message: \"Security scheme must use type:http with scheme:bearer (Solcast API key).\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/solcast/refs/heads/main/rules/solcast-rules.yml
tags:
- Solar
- Energy
- Forecasting
- Irradiance
- Weather
- Renewable Energy
- PV Power
- Spectral
- Linting
- API Governance
---
