---
api_specs:
- filename: webflow-data-api-openapi.yml
  format: yaml
  label: Webflow Data API
  slug: data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-data-api-openapi.yml
- filename: webflow-meta-openapi.yml
  format: yaml
  label: Webflow Meta API
  slug: meta-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-meta-openapi.yml
- filename: webflow-sites-openapi.yml
  format: yaml
  label: Webflow Sites API
  slug: sites-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-sites-openapi.yml
- filename: webflow-pages-openapi.yml
  format: yaml
  label: Webflow Pages API
  slug: pages-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-pages-openapi.yml
- filename: webflow-collections-openapi.yml
  format: yaml
  label: Webflow Collections API
  slug: collections-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-collections-openapi.yml
- filename: webflow-items-openapi.yml
  format: yaml
  label: Webflow CMS Items API
  slug: items-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-items-openapi.yml
- filename: webflow-components-openapi.yml
  format: yaml
  label: Webflow Components API
  slug: components-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-components-openapi.yml
- filename: webflow-assets-openapi.yml
  format: yaml
  label: Webflow Assets API
  slug: assets-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-assets-openapi.yml
- filename: webflow-forms-openapi.yml
  format: yaml
  label: Webflow Forms API
  slug: forms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-forms-openapi.yml
- filename: webflow-products-openapi.yml
  format: yaml
  label: Webflow Products and SKUs API
  slug: products-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-products-openapi.yml
- filename: webflow-orders-openapi.yml
  format: yaml
  label: Webflow Orders API
  slug: orders-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-orders-openapi.yml
- filename: webflow-inventory-openapi.yml
  format: yaml
  label: Webflow Inventory API
  slug: inventory-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-inventory-openapi.yml
- filename: webflow-ecommerce-settings-openapi.yml
  format: yaml
  label: Webflow Ecommerce Settings API
  slug: ecommerce-settings-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-ecommerce-settings-openapi.yml
- filename: webflow-webhooks-openapi.yml
  format: yaml
  label: Webflow Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-webhooks-openapi.yml
- filename: webflow-custom-code-openapi.yml
  format: yaml
  label: Webflow Custom Code API
  slug: custom-code-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-custom-code-openapi.yml
- filename: webflow-comments-openapi.yml
  format: yaml
  label: Webflow Comments API
  slug: comments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-comments-openapi.yml
categories:
- delete
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Webflow.
layout: rules
name: Webflow API Rules
provider_name: Webflow
provider_slug: webflow
rule_count: 26
rules:
- description: API title must start with "Webflow" to match provider naming convention.
  given: $.info
  name: info-title-webflow-prefix
  severity: warn
- description: API must have a non-empty description.
  given: $.info
  name: info-description-required
  severity: warn
- description: API info must include a version.
  given: $.info
  name: info-version-required
  severity: error
- description: Webflow API specs must use OpenAPI 3.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: warn
- description: Server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Webflow API servers must use the api.webflow.com domain.
  given: $.servers[*]
  name: servers-webflow-domain
  severity: info
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Webflow path segments use snake_case (underscores).
  given: $.paths[*]~
  name: paths-snake-case-segments
  severity: info
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with an uppercase letter.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Operation IDs in Webflow APIs use kebab-case.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-kebab-case
  severity: info
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Request bodies must define application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-type
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: warn
- description: Operations should define 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-error-401
  severity: info
- description: Webflow API schema properties use camelCase naming.
  given: $.components.schemas[*].properties[*]~
  name: schema-camelcase-properties
  severity: info
- description: Component schemas should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
- description: Security schemes must be defined.
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: Webflow uses OAuth 2.0 and API key authentication.
  given: $.components.securitySchemes[*].type
  name: security-oauth2-or-apikey
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204 No Content.
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: error
rules_file: rules/webflow-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/rules/webflow-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 8
  warn: 10
slug: webflow-spectral-rules
source_filename: webflow-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-webflow-prefix:\n    description: API title must start with \"Webflow\" to match provider naming convention.\n    message: \"{{property}} title should start with 'Webflow'\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: title\n      function: pattern\n      functionOptions:\n        match: \"^Webflow\"\n\n  info-description-required:\n    description: API must have a non-empty description.\n    message: \"{{property}} description is required\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API info must include a version.\n    message: \"{{property}} must have a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: Webflow API specs must use OpenAPI 3.x.\n    message: \"{{property}} must be OpenAPI\
  \ 3.x\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    message: \"{{property}} servers must be defined\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: Server URLs must use HTTPS.\n    message: \"{{value}} must use HTTPS\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-webflow-domain:\n    description: Webflow API servers must use the api.webflow.com domain.\n    message: \"{{value}} should use api.webflow.com\"\n    severity: info\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"api\\\\.webflow\\\\.com\"\n\n  #\
  \ PATHS — NAMING CONVENTIONS\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    message: \"{{property}} must not end with a slash\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-snake-case-segments:\n    description: Webflow path segments use snake_case (underscores).\n    message: \"{{property}} path segments should use snake_case\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z]\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    message: \"{{property}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries must start with an uppercase\
  \ letter.\n    message: \"{{property}} summary must start with uppercase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-id-required:\n    description: Every operation must have an operationId.\n    message: \"{{property}} must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-kebab-case:\n    description: Operation IDs in Webflow APIs use kebab-case.\n    message: \"{{value}} operationId should use kebab-case\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    message: \"{{property}} must have at least one tag\"\
  \n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter must have a description.\n    message: \"{{property}} parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-content-type:\n    description: Request bodies must define application/json content type.\n    message: \"{{property}} request body should define application/json\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    message: \"{{property}} must have a success response\"\n    severity:\
  \ error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  response-description-required:\n    description: Every response must have a description.\n    message: \"{{property}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  response-error-401:\n    description: Operations should define 401 Unauthorized response.\n    message: \"{{property}} should include 401 Unauthorized\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-camelcase-properties:\n    description: Webflow API schema properties use camelCase naming.\n\
  \    message: \"{{property}} should use camelCase\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_\"\n\n  schema-description-recommended:\n    description: Component schemas should have descriptions.\n    message: \"{{property}} should have a description\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined.\n    message: \"{{property}} must define security schemes\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-oauth2-or-apikey:\n    description: Webflow uses OAuth 2.0 and API key authentication.\n    message: \"{{property}} must use OAuth2 or ApiKey scheme\"\n    severity: info\n    given: \"$.components.securitySchemes[*].type\"\n\
  \    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - oauth2\n          - apiKey\n          - http\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    message: \"{{property}} GET must not have requestBody\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-returns-204:\n    description: DELETE operations should return 204 No Content.\n    message: \"{{property}} DELETE should return 204\"\n    severity: info\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings.\n    message: \"{{property}} description must not be empty\"\n    severity: error\n    given: \"$..description\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/rules/webflow-spectral-rules.yml
tags:
- CMS
- Ecommerce
- No-Code
- Web Development
- Spectral
- Linting
- API Governance
---
