---
api_specs:
- filename: usgs-earthquake-api-openapi.yaml
  format: yaml
  label: Earthquake Notifications, Feeds, and Web Services
  slug: earthquake-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/u-s-geological-survey/refs/heads/main/openapi/usgs-earthquake-api-openapi.yaml
- filename: usgs-water-data-api-openapi.yaml
  format: yaml
  label: USGS Water Data APIs
  slug: water-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/u-s-geological-survey/refs/heads/main/openapi/usgs-water-data-api-openapi.yaml
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tags
- usgs
description: Spectral linting rules defining API design standards and conventions for U.S. Geological Survey.
layout: rules
name: U.S. Geological Survey API Rules
provider_name: U.S. Geological Survey
provider_slug: u-s-geological-survey
rule_count: 33
rules:
- description: API title must be present and include "USGS".
  given: $.info.title
  name: info-title-required
  severity: error
- description: API description must be at least 50 characters.
  given: $.info
  name: info-description-min-length
  severity: warn
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information should be present.
  given: $.info
  name: info-contact-required
  severity: warn
- description: License information should be present for government APIs.
  given: $.info
  name: info-license-required
  severity: info
- description: USGS API specs must use OpenAPI 3.0.x.
  given: $
  name: openapi-version-3
  severity: warn
- description: At least one server URL must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Server URLs should reference usgs.gov domains.
  given: $.servers[*].url
  name: servers-usgs-domain
  severity: info
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths should not end with a trailing slash (except root).
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: info
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "USGS".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined with descriptions.
  given: $
  name: tags-global-defined
  severity: info
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must define a schema.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Format parameter values should use lowercase identifiers.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'f')].schema.enum[*]
  name: parameter-format-lowercase
  severity: info
- description: All operations must define a 200 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 400 error response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-400-defined
  severity: warn
- description: Authenticated operations should define a 403 error response.
  given: $.paths[*][get,post].responses
  name: response-403-defined
  severity: info
- description: All response definitions must have descriptions.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: warn
- description: Component schemas should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: GeoJSON Feature and FeatureCollection schemas should document the 'type' property.
  given: $.components.schemas[?(@.title =~ /Feature|Collection/)].properties
  name: schema-geojson-type-documented
  severity: info
- description: API key security schemes should be defined in components.
  given: $.components.securitySchemes
  name: security-scheme-defined
  severity: warn
- description: API key security scheme should describe how to obtain the key.
  given: $.components.securitySchemes[*]
  name: security-api-key-documented
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: OGC API endpoints should support the 'f' format parameter.
  given: $.paths[*].get.parameters[*].name
  name: usgs-ogc-format-parameter
  severity: info
- description: APIs with API key auth should document 429 responses.
  given: $.paths[*][get,post].responses
  name: usgs-rate-limit-documented
  severity: info
- description: Descriptions should not be empty.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/usgs-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/u-s-geological-survey/refs/heads/main/rules/usgs-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 10
  warn: 14
slug: usgs-spectral-rules
source_filename: usgs-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and include \"USGS\".\n    severity: error\n    given: $.info.title\n    then:\n      function: truthy\n\n  info-description-min-length:\n    description: API description must be at least 50 characters.\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information should be present.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  info-license-required:\n    description: License information should be present for government APIs.\n    severity: info\n    given: $.info\n    then:\n      field: license\n      function:\
  \ truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: USGS API specs must use OpenAPI 3.0.x.\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server URL must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-usgs-domain:\n    description: Server URLs should reference usgs.gov domains.\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"usgs\\\\.gov\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case.\n\
  \    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_.-]*)+$\"\n\n  paths-no-trailing-slash:\n    description: Paths should not end with a trailing slash (except root).\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-prefix:\n    description: Operation summaries should start with \"USGS\".\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^USGS\"\n\n  operation-description-required:\n    description: All operations should have a description.\n    severity: warn\n    given:\
  \ $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: OperationIds should use camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-global-defined:\n    description: Global tags array should be defined with descriptions.\n    severity: info\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n\
  \  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: All parameters must define a schema.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  parameter-format-lowercase:\n    description: Format parameter values should use lowercase identifiers.\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'f')].schema.enum[*]\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z]+$\"\n\n  # RESPONSES\n  response-success-required:\n    description: All operations must define a 200 success response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n\
  \      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"200\"\n\n  response-400-defined:\n    description: Operations should define a 400 error response.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"400\"\n\n  response-403-defined:\n    description: Authenticated operations should define a 403 error response.\n    severity: info\n    given: $.paths[*][get,post].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"403\"\n\n  response-description-required:\n    description: All response definitions must have descriptions.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function:\
  \ truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description: Component schemas should have descriptions.\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-geojson-type-documented:\n    description: GeoJSON Feature and FeatureCollection schemas should document the 'type' property.\n    severity: info\n    given: $.components.schemas[?(@.title =~ /Feature|Collection/)].properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - type\n\n  # SECURITY\n  security-scheme-defined:\n    description: API key security schemes should be defined in components.\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  security-api-key-documented:\n    description: API key security scheme should describe how to obtain the key.\n    severity: info\n    given: $.components.securitySchemes[*]\n\
  \    then:\n      field: description\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # OGC/USGS SPECIFIC\n  usgs-ogc-format-parameter:\n    description: OGC API endpoints should support the 'f' format parameter.\n    severity: info\n    given: $.paths[*].get.parameters[*].name\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: string\n\n  usgs-rate-limit-documented:\n    description: APIs with API key auth should document 429 responses.\n    severity: info\n    given: $.paths[*][get,post].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"429\"\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions should not be empty.\n\
  \    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".{1,}\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/u-s-geological-survey/refs/heads/main/rules/usgs-spectral-rules.yml
tags:
- Federal Government
- Geological
- Earth Science
- Natural Resources
- Earthquake
- Water
- Hydrology
- Spectral
- Linting
- API Governance
---
