---
api_specs:
- filename: toast-orders-openapi.yaml
  format: yaml
  label: Toast Orders API
  slug: toast-orders
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-orders-openapi.yaml
- filename: toast-menus-openapi.yaml
  format: yaml
  label: Toast Menus API
  slug: toast-menus
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-menus-openapi.yaml
- filename: toast-labor-openapi.yaml
  format: yaml
  label: Toast Labor API
  slug: toast-labor
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-labor-openapi.yaml
- filename: toast-restaurants-openapi.yaml
  format: yaml
  label: Toast Restaurants API
  slug: toast-restaurants
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-restaurants-openapi.yaml
- filename: toast-stock-openapi.yaml
  format: yaml
  label: Toast Stock API
  slug: toast-stock
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-stock-openapi.yaml
- filename: toast-partners-openapi.yaml
  format: yaml
  label: Toast Partners API
  slug: toast-partners
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-partners-openapi.yaml
- filename: toast-authentication-openapi.yaml
  format: yaml
  label: Toast Authentication API
  slug: toast-authentication
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/openapi/toast-authentication-openapi.yaml
categories:
- delete
- examples
- get
- info
- 'no'
- operation
- parameter
- paths
- response
- schema
- security
- servers
- toast
description: Spectral linting rules defining API design standards and conventions for Toast.
layout: rules
name: Toast API Rules
provider_name: Toast
provider_slug: toast
rule_count: 29
rules:
- description: Info object must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with 'Toast'
  given: $.info.title
  name: info-title-toast-prefix
  severity: warn
- description: Info object must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Info object must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Paths must not end with a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Path parameters for identifiers should use 'guid' naming
  given: $.paths[*]~
  name: paths-guid-parameters
  severity: info
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with 'Toast'
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-toast-prefix
  severity: info
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: OperationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: info
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete][parameters][*]
  name: parameter-description-required
  severity: warn
- description: Restaurant GUID should be passed as a header named Toast-Restaurant-External-ID
  given: $.paths[*][get,post,put,patch,delete][parameters][*][?(@.name=='restaurantGuid')]
  name: parameter-restaurant-guid-header
  severity: info
- description: Operations must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All response objects must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Secured operations should define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-defined
  severity: info
- description: GET by ID operations should define a 404 Not Found response
  given: $.paths[*~*Guid*][get].responses
  name: response-404-on-get-by-id
  severity: info
- description: Schema property names should use camelCase
  given: $.definitions[*].properties[*]~
  name: schema-property-camel-case
  severity: info
- description: Top-level schemas should have a description
  given: $.definitions[*]
  name: schema-description-required
  severity: info
- description: Properties named 'guid' should have format uuid
  given: $.definitions[*].properties[?(@property === 'guid')]
  name: schema-guid-property-format
  severity: info
- description: Security should be defined at the API level
  given: $
  name: security-defined
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: delete-returns-no-content
  severity: info
- description: Most Toast APIs require Toast-Restaurant-External-ID header
  given: $.paths[*][get,post,put,patch].parameters
  name: toast-restaurant-guid-required
  severity: info
- description: Description fields must not be empty
  given:
  - $.info.description
  - $.paths[*][get,post,put,patch,delete].description
  name: no-empty-descriptions
  severity: error
- description: Schema properties should have example values
  given: $.definitions[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/toast-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/rules/toast-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 13
  warn: 6
slug: toast-spectral-rules
source_filename: toast-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: Info object must have a title\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-toast-prefix:\n    description: API title should start with 'Toast'\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Toast\"\n\n  info-description-required:\n    description: Info object must have a description\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: Info object must have a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # SERVERS\n  servers-defined:\n    description: Servers array must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n\
  \    description: Server URLs must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS - NAMING CONVENTIONS\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-guid-parameters:\n    description: Path parameters for identifiers should use 'guid' naming\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\{id\\\\}\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-toast-prefix:\n    description: Operation summaries\
  \ should start with 'Toast'\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Toast\"\n\n  operation-operationid-required:\n    description: Every operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camel-case:\n    description: OperationId should use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  operation-description-required:\n    description: Operations should have\
  \ a description\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete][parameters][*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-restaurant-guid-header:\n    description: Restaurant GUID should be passed as a header named Toast-Restaurant-External-ID\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete][parameters][*][?(@.name=='restaurantGuid')]\"\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values: [\"header\"]\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least one 2xx response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  response-description-required:\n    description: All response objects must have a description\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  response-401-defined:\n    description: Secured operations should define a 401 Unauthorized response\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"401\"]\n\n  response-404-on-get-by-id:\n    description: GET by ID operations should define a 404 Not Found response\n    severity: info\n    given: \"$.paths[*~*Guid*][get].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"404\"]\n\n  # SCHEMAS - PROPERTY\
  \ NAMING\n  schema-property-camel-case:\n    description: Schema property names should use camelCase\n    severity: info\n    given: \"$.definitions[*].properties[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  schema-description-required:\n    description: Top-level schemas should have a description\n    severity: info\n    given: \"$.definitions[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-guid-property-format:\n    description: Properties named 'guid' should have format uuid\n    severity: info\n    given: \"$.definitions[*].properties[?(@property === 'guid')]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values: [\"uuid\"]\n\n  # SECURITY\n  security-defined:\n    description: Security should be defined at the API level\n    given: \"$\"\n    severity: info\n    then:\n      field: securityDefinitions\n      function: truthy\n\n  # HTTP METHOD\
  \ CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: body\n      function: falsy\n\n  delete-returns-no-content:\n    description: DELETE operations should return 204 No Content\n    severity: info\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"204\"]\n\n  # TOAST-SPECIFIC CONVENTIONS\n  toast-restaurant-guid-required:\n    description: Most Toast APIs require Toast-Restaurant-External-ID header\n    severity: info\n    given: \"$.paths[*][get,post,put,patch].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                enum: [\"Toast-Restaurant-External-ID\"]\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n\
  \    description: Description fields must not be empty\n    severity: error\n    given:\n      - \"$.info.description\"\n      - \"$.paths[*][get,post,put,patch,delete].description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\S\"\n\n  examples-encouraged:\n    description: Schema properties should have example values\n    severity: info\n    given: \"$.definitions[*].properties[*]\"\n    then:\n      field: example\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toast/refs/heads/main/rules/toast-spectral-rules.yml
tags:
- Food Service
- Point of Sale
- Restaurants
- Hospitality
- Spectral
- Linting
- API Governance
---
