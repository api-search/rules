---
api_specs:
- filename: webex-messaging-openapi.json
  format: json
  label: Webex Messaging
  slug: messaging
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-messaging-openapi.json
- filename: webex-meeting-openapi.json
  format: json
  label: Webex Meetings
  slug: meetings
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-meeting-openapi.json
- filename: webex-admin-openapi.json
  format: json
  label: Webex Admin
  slug: admin
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-admin-openapi.json
- filename: webex-cloud-calling-openapi.json
  format: json
  label: Webex Cloud Calling
  slug: cloud-calling
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-cloud-calling-openapi.json
- filename: webex-contact-center-openapi.json
  format: json
  label: Webex Contact Center
  slug: contact-center
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-contact-center-openapi.json
- filename: webex-device-openapi.json
  format: json
  label: Webex Devices
  slug: devices
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-device-openapi.json
- filename: webex-broadworks-openapi.json
  format: json
  label: Webex Broadworks Calling
  slug: broadworks
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-broadworks-openapi.json
- filename: webex-ucm-openapi.json
  format: json
  label: Webex for UCM
  slug: ucm
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-ucm-openapi.json
- filename: webex-wholesale-openapi.json
  format: json
  label: Webex Wholesale
  slug: wholesale
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/openapi/webex-wholesale-openapi.json
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
- tags
description: Spectral linting rules defining API design standards and conventions for Webex.
layout: rules
name: Webex API Rules
provider_name: Webex
provider_slug: webex
rule_count: 29
rules:
- description: API title must be present and follow "Webex {Product}" naming convention.
  given: $.info
  name: info-title-required
  severity: error
- description: API must have a non-empty description of at least 20 characters.
  given: $.info
  name: info-description-required
  severity: warn
- description: API info must include a version field.
  given: $.info
  name: info-version-required
  severity: error
- description: All Webex API specs must use OpenAPI 3.0.x or 3.1.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: warn
- description: Server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https-only
  severity: error
- description: Path must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Path segments must use camelCase or kebab-case (no underscores or uppercase).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-id-required
  severity: error
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Tag names must use Title Case (e.g., "Attachment Actions", "Room Types").
  given: $.tags[*].name
  name: tags-title-case
  severity: warn
- description: Global tags should have descriptions.
  given: $.tags[*]
  name: tags-description-required
  severity: info
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter schema must have a type.
  given: $.paths[*][get,post,put,patch,delete].parameters[*].schema
  name: parameter-schema-type-required
  severity: warn
- description: Request bodies must include an application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-content-type
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define 400 or 401 error responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-4xx-required
  severity: info
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: warn
- description: Top-level component schemas should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Schema properties should have a type defined.
  given: $.components.schemas[*].properties[*]
  name: schema-properties-type-defined
  severity: info
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: Webex APIs use Bearer token or OAuth2 authentication.
  given: $.components.securitySchemes[*]
  name: security-bearer-or-oauth2
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body.
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: No descriptions should be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Operations should include request/response examples.
  given: $.paths[*][post,put,patch].requestBody.content.application/json
  name: operation-examples-encouraged
  severity: info
rules_file: rules/webex-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/rules/webex-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 6
  warn: 14
slug: webex-spectral-rules
source_filename: webex-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and follow \"Webex {Product}\" naming convention.\n    message: \"{{property}} must be present and start with 'Webex'\"\n    severity: error\n    given: \"$.info\"\n    then:\n      - field: title\n        function: truthy\n      - field: title\n        function: pattern\n        functionOptions:\n          match: \"^Webex\"\n\n  info-description-required:\n    description: API must have a non-empty description of at least 20 characters.\n    message: \"{{property}} description is required and must be at least 20 characters\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        value: 20\n\n  info-version-required:\n    description: API info must include a version field.\n    message: \"{{property}} must have a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n\
  \      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: All Webex API specs must use OpenAPI 3.0.x or 3.1.x.\n    message: \"{{property}} must be OpenAPI 3.x\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    message: \"{{property}} servers array must be defined and non-empty\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-only:\n    description: Server URLs must use HTTPS.\n    message: \"{{value}} server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-no-trailing-slash:\n    description: Path must not end with a trailing slash.\n\
  \    message: \"{{property}} path must not have a trailing slash\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-kebab-case:\n    description: Path segments must use camelCase or kebab-case (no underscores or uppercase).\n    message: \"{{property}} path segment must use camelCase or kebab-case\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"_\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    message: \"{{property}} operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"{{property}} summary must start with an uppercase\
  \ letter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    message: \"{{property}} operation must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: Every operation must have an operationId.\n    message: \"{{property}} operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    message: \"{{property}} operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-title-case:\n    description: Tag names must use Title Case (e.g., \"Attachment Actions\", \"Room Types\").\n    message: \"{{value}} tag name must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  tags-description-required:\n    description: Global tags should have descriptions.\n    message: \"{{property}} tag should have a description\"\n    severity: info\n    given: \"$.tags[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter must have a description.\n    message: \"{{property}} parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-type-required:\n \
  \   description: Every parameter schema must have a type.\n    message: \"{{property}} parameter schema must define a type\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*].schema\"\n    then:\n      field: type\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-json-content-type:\n    description: Request bodies must include an application/json content type.\n    message: \"{{property}} request body should define application/json content\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    message: \"{{property}} operation must have a 2xx success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  response-4xx-required:\n    description: Operations should define 400 or 401 error responses.\n    message: \"{{property}} operation should include error response codes\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n\n  response-description-required:\n    description: Every response must have a description.\n    message: \"{{property}} response must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description:\
  \ Top-level component schemas should have descriptions.\n    message: \"{{property}} schema should have a description\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-type-defined:\n    description: Schema properties should have a type defined.\n    message: \"{{property}} schema property should define a type\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    message: \"{{property}} components must define security schemes\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-bearer-or-oauth2:\n    description: Webex APIs use Bearer token or OAuth2 authentication.\n    message: \"{{property}} security scheme must be bearer or\
  \ oauth2\"\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - properties:\n                type:\n                  const: http\n              required: [type]\n            - properties:\n                type:\n                  const: oauth2\n              required: [type]\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    message: \"{{property}} GET operation must not have a requestBody\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body.\n    message: \"{{property}} DELETE operation should not have a requestBody\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  #\
  \ GENERAL QUALITY\n  no-empty-descriptions:\n    description: No descriptions should be empty strings.\n    message: \"{{property}} description must not be an empty string\"\n    severity: error\n    given: \"$..description\"\n    then:\n      function: truthy\n\n  operation-examples-encouraged:\n    description: Operations should include request/response examples.\n    message: \"{{property}} operation should include examples for documentation\"\n    severity: info\n    given: \"$.paths[*][post,put,patch].requestBody.content.application/json\"\n    then:\n      field: example\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/webex/refs/heads/main/rules/webex-spectral-rules.yml
tags:
- Calling
- Collaboration
- Communication
- Enterprise
- Messaging
- Video Conferencing
- Spectral
- Linting
- API Governance
---
