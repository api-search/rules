---
api_specs:
- filename: varonis-datalert-openapi.yml
  format: yaml
  label: Varonis DatAlert API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/varonis/refs/heads/main/openapi/varonis-datalert-openapi.yml
categories:
- get
- info
- 'no'
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
description: Spectral linting rules defining API design standards and conventions for Varonis.
layout: rules
name: Varonis API Rules
provider_name: Varonis
provider_slug: varonis
rule_count: 34
rules:
- description: API title must be present and non-empty.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Varonis".
  given: $.info.title
  name: info-title-starts-with-varonis
  severity: warn
- description: API description must be present and non-empty.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information should be present.
  given: $.info
  name: info-contact-required
  severity: warn
- description: API specification must use OpenAPI 3.x.
  given: $
  name: openapi-version-3x
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-required
  severity: error
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-operationId-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Varonis".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-varonis
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-description-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined.
  given: $
  name: tags-global-defined
  severity: warn
- description: Each global tag should have a description.
  given: $.tags[*]
  name: tags-description-required
  severity: warn
- description: All parameters must have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema with a type.
  given: $..parameters[*].schema
  name: parameter-schema-type-required
  severity: error
- description: Request bodies should have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description-required
  severity: warn
- description: POST/PUT/PATCH operations should accept application/json.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-json
  severity: warn
- description: Operations must define at least one success (2xx) response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: POST operations with request bodies should define 400 Bad Request.
  given: $.paths[*].post.responses
  name: response-400-for-post
  severity: warn
- description: Operations should define 401 Unauthorized.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: All responses must have a description.
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schema definitions should have a description.
  given: $.components.schemas[*]
  name: schema-property-description-required
  severity: warn
- description: Schema properties should have explicit types.
  given: $.components.schemas[*].properties[*]
  name: schema-properties-have-types
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security should be defined.
  given: $
  name: security-global-defined
  severity: warn
- description: API keys should be passed in headers, not query parameters.
  given: $.components.securitySchemes[?(@.type == 'apiKey')]
  name: security-apikey-header-not-query
  severity: error
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should typically have a request body.
  given: $.paths[*].post
  name: post-should-have-request-body
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-description
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
rules_file: rules/varonis-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/varonis/refs/heads/main/rules/varonis-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 1
  warn: 20
slug: varonis-spectral-rules
source_filename: varonis-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and non-empty.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-starts-with-varonis:\n    description: API title should start with \"Varonis\".\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Varonis\"\n\n  info-description-required:\n    description: API description must be present and non-empty.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information should be present.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n\
  \      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3x:\n    description: API specification must use OpenAPI 3.x.\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: At least one server must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-required:\n    description: Server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description-required:\n    description: Each server should have a description.\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # OPERATIONS\n  operation-operationId-required:\n    description: All operations must have an operationId.\n \
  \   severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camelCase:\n    description: operationId must use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-starts-with-varonis:\n    description: Operation summaries should start with \"Varonis\".\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Varonis \"\n\n  operation-description-required:\n    description: All operations\
  \ must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-global-defined:\n    description: Global tags array should be defined.\n    severity: warn\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\n  tags-description-required:\n    description: Each global tag should have a description.\n    severity: warn\n    given: \"$.tags[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\
  \n  parameter-schema-type-required:\n    description: All parameters must have a schema with a type.\n    severity: error\n    given: \"$..parameters[*].schema\"\n    then:\n      field: type\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-description-required:\n    description: Request bodies should have a description.\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  request-body-content-json:\n    description: POST/PUT/PATCH operations should accept application/json.\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least one success (2xx) response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['202']\n            - required: ['204']\n\n  response-400-for-post:\n    description: POST operations with request bodies should define 400 Bad Request.\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: '400'\n      function: truthy\n\n  response-401-required:\n    description: Operations should define 401 Unauthorized.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  response-description-required:\n    description: All responses must have a description.\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-property-description-required:\n    description: Top-level schema definitions should have a description.\n    severity: warn\n    given:\
  \ \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-have-types:\n    description: Schema properties should have explicit types.\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-global-defined:\n    description: Global security should be defined.\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  security-apikey-header-not-query:\n    description: API keys should be passed in headers, not query parameters.\n    severity: error\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')]\"\n    then:\n      field: in\n      function: pattern\n      functionOptions:\n\
  \        match: \"^header$\"\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  post-should-have-request-body:\n    description: POST operations should typically have a request body.\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-description:\n    description: Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/varonis/refs/heads/main/rules/varonis-spectral-rules.yml
tags:
- Cloud Security
- Compliance
- Data Analytics
- Data Governance
- Data Security
- Threat Detection
- Spectral
- Linting
- API Governance
---
