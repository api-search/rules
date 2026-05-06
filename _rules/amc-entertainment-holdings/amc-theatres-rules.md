---
api_specs:
- filename: amc-theatres-api-openapi.yml
  format: yaml
  label: AMC Theatres API
  slug: amc-theatres-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/amc-entertainment-holdings/refs/heads/main/openapi/amc-theatres-api-openapi.yml
categories:
- amc
description: Spectral linting rules defining API design standards and conventions for AMC Entertainment Holdings.
layout: rules
name: AMC Entertainment Holdings API Rules
provider_name: AMC Entertainment Holdings
provider_slug: amc-entertainment-holdings
rule_count: 28
rules:
- description: API title must be present.
  given: $.info
  name: amc-info-title-required
  severity: error
- description: Title should start with "AMC".
  given: $.info.title
  name: amc-info-title-format
  severity: warn
- description: API description should be substantive (>= 80 chars).
  given: $.info.description
  name: amc-info-description-min-length
  severity: warn
- description: Contact information must be provided.
  given: $.info
  name: amc-info-contact-required
  severity: warn
- description: License must be declared (AMC API Terms of Use).
  given: $.info
  name: amc-info-license-required
  severity: warn
- description: At least one server must be defined.
  given: $
  name: amc-servers-required
  severity: error
- description: Server URL must point at api.amctheatres.com.
  given: $.servers[*].url
  name: amc-servers-amctheatres-host
  severity: error
- description: AMC API only supports HTTPS.
  given: $.servers[*].url
  name: amc-servers-https-only
  severity: error
- description: A vendor-key apiKey security scheme must be defined.
  given: $.components.securitySchemes
  name: amc-security-vendor-key-defined
  severity: error
- description: Vendor key must be provided in the X-AMC-Vendor-Key header.
  given: $.components.securitySchemes.VendorKey
  name: amc-security-vendor-key-header
  severity: error
- description: The vendor-key security requirement must be applied globally.
  given: $
  name: amc-security-applied-globally
  severity: error
- description: All paths must be versioned (/v1, /v2, /v3, /v4).
  given: $.paths.*~
  name: amc-paths-versioned
  severity: error
- description: Path segments (excluding parameters) must be kebab-case.
  given: $.paths.*~
  name: amc-paths-kebab-case
  severity: warn
- description: Paths should not end with a trailing slash (except documented order email lookup).
  given: $.paths.*~
  name: amc-paths-no-trailing-slash
  severity: warn
- description: Every operation must declare an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: amc-operation-operationId-required
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: amc-operation-operationId-camelcase
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: amc-operation-summary-required
  severity: error
- description: Summary should use Title Case.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: amc-operation-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: amc-operation-tags-required
  severity: warn
- description: Tag names use Title Case (e.g., Theatres, Showtimes, Loyalty).
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: amc-operation-tag-titlecase
  severity: warn
- description: Read operations should declare a 200 response.
  given: $.paths[*].get.responses
  name: amc-operation-200-response
  severity: warn
- description: POST operations that create resources should return 201.
  given: $.paths[?(@property.match(/orders|webhooks|registration|redemptions/))].post.responses
  name: amc-operation-201-on-create
  severity: info
- description: Query and path parameter names should use kebab-case (page-size, theatre-number, etc.).
  given: $..parameters[?(@.in == 'query' || @.in == 'path')].name
  name: amc-parameter-name-kebab-case
  severity: warn
- description: When page-size is used, page-number should also be available.
  given: $.paths[*][get]
  name: amc-parameter-pagination-pair
  severity: info
- description: Collection schemas should include pageSize, pageNumber, count, and _embedded.
  given: $.components.schemas[?(@property.match(/Collection$/))].allOf[0]
  name: amc-schemas-collection-envelope
  severity: info
- description: Resources should expose HAL-style _links where applicable.
  given: $.components.schemas
  name: amc-schemas-hal-links
  severity: info
- description: Schema properties should use camelCase.
  given: $.components.schemas[*].properties.*~
  name: amc-schemas-property-camelcase
  severity: warn
- description: Error responses should reference the ApiError schema.
  given: $.components.responses.NotFound.content['application/json'].schema
  name: amc-responses-error-content
  severity: info
rules_file: rules/amc-theatres-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/amc-entertainment-holdings/refs/heads/main/rules/amc-theatres-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 5
  warn: 13
slug: amc-theatres-rules
source_filename: amc-theatres-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral ruleset for the AMC Theatres API.\n# Reflects conventions observed in developers.amctheatres.com:\n# - Resources are under /v1, /v2, /v3, /v4 prefixes per resource family\n# - Auth is via the X-AMC-Vendor-Key header (apiKey)\n# - Collection responses use HAL-style _embedded + pageSize/pageNumber/count\n# - Path segments and query parameter names use kebab-case\n# - operationIds use camelCase\n# - tags use Title Case\n\nrules:\n\n  # =============================================================\n  # INFO / METADATA\n  # =============================================================\n\n  amc-info-title-required:\n    description: API title must be present.\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  amc-info-title-format:\n    description: Title should start with \"AMC\".\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n    \
  \    match: \"^AMC \"\n\n  amc-info-description-min-length:\n    description: API description should be substantive (>= 80 chars).\n    severity: warn\n    given: $.info.description\n    then:\n      function: length\n      functionOptions:\n        min: 80\n\n  amc-info-contact-required:\n    description: Contact information must be provided.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  amc-info-license-required:\n    description: License must be declared (AMC API Terms of Use).\n    severity: warn\n    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  # =============================================================\n  # SERVERS\n  # =============================================================\n\n  amc-servers-required:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  amc-servers-amctheatres-host:\n   \
  \ description: Server URL must point at api.amctheatres.com.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.amctheatres\\\\.com\"\n\n  amc-servers-https-only:\n    description: AMC API only supports HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # =============================================================\n  # SECURITY\n  # =============================================================\n\n  amc-security-vendor-key-defined:\n    description: A vendor-key apiKey security scheme must be defined.\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      field: VendorKey\n      function: truthy\n\n  amc-security-vendor-key-header:\n    description: Vendor key must be provided in the X-AMC-Vendor-Key header.\n    severity: error\n    given: $.components.securitySchemes.VendorKey\n\
  \    then:\n      - field: type\n        function: pattern\n        functionOptions:\n          match: \"^apiKey$\"\n      - field: in\n        function: pattern\n        functionOptions:\n          match: \"^header$\"\n      - field: name\n        function: pattern\n        functionOptions:\n          match: \"^X-AMC-Vendor-Key$\"\n\n  amc-security-applied-globally:\n    description: The vendor-key security requirement must be applied globally.\n    severity: error\n    given: $\n    then:\n      field: security\n      function: truthy\n\n  # =============================================================\n  # PATHS\n  # =============================================================\n\n  amc-paths-versioned:\n    description: All paths must be versioned (/v1, /v2, /v3, /v4).\n    severity: error\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[1-4](/|$)\"\n\n  amc-paths-kebab-case:\n    description: Path segments (excluding parameters)\
  \ must be kebab-case.\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[1-4])(/(\\\\{[a-zA-Z][a-zA-Z0-9_-]*\\\\}|[a-z][a-z0-9-]*))*/?$\"\n\n  amc-paths-no-trailing-slash:\n    description: Paths should not end with a trailing slash (except documented order email lookup).\n    severity: warn\n    given: $.paths.*~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[a-z0-9}]/$\"\n\n  # =============================================================\n  # OPERATIONS\n  # =============================================================\n\n  amc-operation-operationId-required:\n    description: Every operation must declare an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  amc-operation-operationId-camelcase:\n    description: operationId must be camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  amc-operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: truthy\n\n  amc-operation-summary-title-case:\n    description: Summary should use Title Case.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-zA-Z0-9]*)( ([A-Z][a-zA-Z0-9]*|[a-z]{1,3}|By|For|To|And|Or|In|On|Of))*$\"\n\n  amc-operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: truthy\n\n  amc-operation-tag-titlecase:\n    description: Tag names use Title Case (e.g., Theatres, Showtimes, Loyalty).\n    severity: warn\n\
  \    given: $.paths[*][get,post,put,delete,patch].tags[*]\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*$\"\n\n  amc-operation-200-response:\n    description: Read operations should declare a 200 response.\n    severity: warn\n    given: $.paths[*].get.responses\n    then:\n      field: '200'\n      function: truthy\n\n  amc-operation-201-on-create:\n    description: POST operations that create resources should return 201.\n    severity: info\n    given: \"$.paths[?(@property.match(/orders|webhooks|registration|redemptions/))].post.responses\"\n    then:\n      field: '201'\n      function: truthy\n\n  # =============================================================\n  # PARAMETERS\n  # =============================================================\n\n  amc-parameter-name-kebab-case:\n    description: Query and path parameter names should use kebab-case (page-size, theatre-number, etc.).\n    severity: warn\n    given: \"$..parameters[?(@.in\
  \ == 'query' || @.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9]*(-[a-z0-9]+)*$\"\n\n  amc-parameter-pagination-pair:\n    description: When page-size is used, page-number should also be available.\n    severity: info\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # =============================================================\n  # SCHEMAS\n  # =============================================================\n\n  amc-schemas-collection-envelope:\n    description: Collection schemas should include pageSize, pageNumber, count, and _embedded.\n    severity: info\n    given: $.components.schemas[?(@property.match(/Collection$/))].allOf[0]\n    then:\n      function: truthy\n\n  amc-schemas-hal-links:\n    description: Resources should expose HAL-style _links where applicable.\n    severity: info\n    given: $.components.schemas\n    then:\n\
  \      field: HalLinks\n      function: truthy\n\n  amc-schemas-property-camelcase:\n    description: Schema properties should use camelCase.\n    severity: warn\n    given: $.components.schemas[*].properties.*~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # =============================================================\n  # RESPONSES\n  # =============================================================\n\n  amc-responses-error-content:\n    description: Error responses should reference the ApiError schema.\n    severity: info\n    given: \"$.components.responses.NotFound.content['application/json'].schema\"\n    then:\n      field: $ref\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/amc-entertainment-holdings/refs/heads/main/rules/amc-theatres-rules.yml
tags:
- Entertainment
- Movies
- Theatres
- Showtimes
- Ticketing
- Concessions
- Loyalty
- Fortune 500
- Spectral
- Linting
- API Governance
---
