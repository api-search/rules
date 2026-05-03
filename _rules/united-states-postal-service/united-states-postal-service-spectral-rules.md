---
api_specs:
- filename: united-states-postal-service-addresses-openapi.yml
  format: yaml
  label: USPS Addresses API
  slug: usps-addresses-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/openapi/united-states-postal-service-addresses-openapi.yml
- filename: united-states-postal-service-tracking-openapi.yml
  format: yaml
  label: USPS Tracking API
  slug: usps-tracking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/openapi/united-states-postal-service-tracking-openapi.yml
- filename: united-states-postal-service-domestic-prices-openapi.yml
  format: yaml
  label: USPS Domestic Prices API
  slug: usps-domestic-prices-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/openapi/united-states-postal-service-domestic-prices-openapi.yml
- filename: united-states-postal-service-carrier-pickup-openapi.yml
  format: yaml
  label: USPS Carrier Pickup API
  slug: usps-carrier-pickup-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/openapi/united-states-postal-service-carrier-pickup-openapi.yml
categories:
- delete
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- post
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for United States Postal Service.
layout: rules
name: United States Postal Service API Rules
provider_name: United States Postal Service
provider_slug: united-states-postal-service
rule_count: 33
rules:
- description: API title must be present and start with USPS.
  given: $.info.title
  name: info-title-required
  severity: error
- description: API info description must be present and at least 50 characters.
  given: $.info.description
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info.version
  name: info-version-required
  severity: error
- description: API info should include contact information.
  given: $.info.contact
  name: info-contact-required
  severity: warn
- description: All USPS API specs should use OpenAPI 3.1.0.
  given: $.openapi
  name: openapi-version
  severity: warn
- description: Servers array must be defined.
  given: $.servers
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Each server should have a description.
  given: $.servers[*].description
  name: servers-description-required
  severity: warn
- description: USPS API servers must use apis.usps.com or apis-tem.usps.com domains.
  given: $.servers[*].url
  name: servers-usps-domain
  severity: warn
- description: Path segments should use kebab-case.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: USPS API paths should include a version segment (e.g., /v3/).
  given: $.paths[*]~
  name: paths-versioned
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with USPS.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: operation-tags-required
  severity: error
- description: Global tags array should be defined.
  given: $.tags
  name: tags-global-defined
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should include application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-json
  severity: warn
- description: Every operation must define at least a 2xx response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All authenticated operations should define a 401 response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-401-required
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should define a type.
  given: $.components.schemas[*].properties[*]
  name: schema-property-type-required
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: USPS APIs use OAuth 2.0 Bearer Token authentication.
  given: $.components.securitySchemes.bearerAuth
  name: security-bearer-auth
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get.requestBody
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body.
  given: $.paths[*].delete.requestBody
  name: delete-no-request-body
  severity: warn
- description: POST operations creating resources should have a request body.
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: Operations should include x-microcks-operation for mock server compatibility.
  given: $.paths[*][get,post,put,delete,patch]
  name: microcks-operation-present
  severity: info
rules_file: rules/united-states-postal-service-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/rules/united-states-postal-service-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 1
  warn: 19
slug: united-states-postal-service-spectral-rules
source_filename: united-states-postal-service-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and start with USPS.\n    severity: error\n    given: \"$.info.title\"\n    then:\n      function: truthy\n\n  info-description-required:\n    description: API info description must be present and at least 50 characters.\n    severity: warn\n    given: \"$.info.description\"\n    then:\n      function: minLength\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: \"$.info.version\"\n    then:\n      function: truthy\n\n  info-contact-required:\n    description: API info should include contact information.\n    severity: warn\n    given: \"$.info.contact\"\n    then:\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version:\n    description: All USPS API specs should use OpenAPI 3.1.0.\n    severity: warn\n    given: \"$.openapi\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^3\\\\.1\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers array must be defined.\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: Each server should have a description.\n    severity: warn\n    given: \"$.servers[*].description\"\n    then:\n      function: truthy\n\n  servers-usps-domain:\n    description: USPS API servers must use apis.usps.com or apis-tem.usps.com domains.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"apis\\\\.usps\\\\.com\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments should use kebab-case.\n    severity:\
  \ warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}./]+)+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-versioned:\n    description: USPS API paths should include a version segment (e.g., /v3/).\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]/\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries should start with USPS.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^USPS \"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: OperationIds should use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].tags\"\n    then:\n   \
  \   function: truthy\n\n  # TAGS\n  tags-global-defined:\n    description: Global tags array should be defined.\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: Every parameter must have a schema.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-content-json:\n    description: Request bodies should include application/json content type.\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every\
  \ operation must define at least a 2xx response.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: truthy\n\n  response-401-required:\n    description: All authenticated operations should define a 401 response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description: Top-level schemas should have a description.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-property-type-required:\n    description: Schema properties should define a type.\n\
  \    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  security-bearer-auth:\n    description: USPS APIs use OAuth 2.0 Bearer Token authentication.\n    severity: warn\n    given: \"$.components.securitySchemes.bearerAuth\"\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get.requestBody\"\n    then:\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body.\n    severity: warn\n    given: \"$.paths[*].delete.requestBody\"\n    then:\n      function: falsy\n\n  post-has-request-body:\n    description:\
  \ POST operations creating resources should have a request body.\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # GENERAL QUALITY\n  microcks-operation-present:\n    description: Operations should include x-microcks-operation for mock server compatibility.\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-postal-service/refs/heads/main/rules/united-states-postal-service-spectral-rules.yml
tags:
- Government
- Postal Service
- Shipping
- Logistics
- Address Validation
- Package Tracking
- Spectral
- Linting
- API Governance
---
