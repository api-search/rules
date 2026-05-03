---
categories:
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
- vertx
description: Spectral linting rules defining API design standards and conventions for Vert.x.
layout: rules
name: Vert.x API Rules
provider_name: Vert.x
provider_slug: vert-x
rule_count: 26
rules:
- description: API title must start with "Vert.x" to align with Eclipse Vert.x naming conventions.
  given: $.info.title
  name: info-title-vertx-prefix
  severity: warn
- description: API info object must have a description explaining the component purpose.
  given: $.info
  name: info-description-required
  severity: error
- description: API version should follow Semantic Versioning (MAJOR.MINOR.PATCH).
  given: $.info.version
  name: info-version-semver
  severity: warn
- description: All server URLs must use HTTPS for secure communication.
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: OpenAPI spec must define at least one server.
  given: $
  name: servers-defined
  severity: warn
- description: API paths must use kebab-case for multi-word path segments.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: API paths must not have a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Vert.x" to indicate the provider.
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-vertx-prefix
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationid-required
  severity: error
- description: Operation IDs should use lowerCamelCase naming convention.
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-operationid-camel-case
  severity: warn
- description: All operations must have at least one tag for grouping in documentation.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: All parameters must have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: Query and header parameter names should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query' || @.in == 'header')].name
  name: parameter-name-camel-case
  severity: hint
- description: Operations must define at least one 2xx success response.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: Operations should define error responses for client errors (4xx).
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-error-defined
  severity: warn
- description: All response objects must have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[*]
  name: response-description-required
  severity: error
- description: All schema objects must define a type.
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: All schemas in components must have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should have descriptions for better developer experience.
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: hint
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: API must define security schemes if authentication is required.
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Health check status fields should use UP or DOWN values.
  given: $.components.schemas[?(@.title =~ /.*[Hh]ealth.*/)]..properties.status
  name: vertx-health-check-status-enum
  severity: hint
- description: Async operations should document their callback or event bus behavior.
  given: $.paths[*][post,put,patch].responses[202]
  name: vertx-async-operations-documented
  severity: hint
rules_file: rules/vert-x-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vert-x/refs/heads/main/rules/vert-x-spectral-rules.yml
severity_counts:
  error: 7
  hint: 4
  info: 0
  warn: 15
slug: vert-x-spectral-rules
source_filename: vert-x-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Info Object Rules\n  info-title-vertx-prefix:\n    description: API title must start with \"Vert.x\" to align with Eclipse Vert.x naming conventions.\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Vert\\\\.x\"\n\n  info-description-required:\n    description: API info object must have a description explaining the component purpose.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-semver:\n    description: API version should follow Semantic Versioning (MAJOR.MINOR.PATCH).\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[0-9]+\\\\.[0-9]+\\\\.[0-9]+\"\n\n  # Server Rules\n  servers-https-only:\n    description: All server URLs must use HTTPS for secure communication.\n    severity: error\n    given: \"$.servers[*].url\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-defined:\n    description: OpenAPI spec must define at least one server.\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  # Path Rules\n  paths-kebab-case:\n    description: API paths must use kebab-case for multi-word path segments.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}]+)+$\"\n\n  paths-no-trailing-slash:\n    description: API paths must not have a trailing slash.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # Operation Rules\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: summary\n      function:\
  \ truthy\n\n  operation-summary-vertx-prefix:\n    description: Operation summaries must start with \"Vert.x\" to indicate the provider.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Vert\\\\.x\"\n\n  operation-description-required:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-operationid-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camel-case:\n    description: Operation IDs should use lowerCamelCase naming convention.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: All operations must have at least one tag for grouping in documentation.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Parameter Rules\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-name-camel-case:\n    description: Query and header parameter names should use camelCase.\n    severity: hint\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query' || @.in == 'header')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9-]*$\"\n\n  # Response Rules\n  response-success-required:\n    description: Operations\
  \ must define at least one 2xx success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required: [\"204\"]\n\n  response-error-defined:\n    description: Operations should define error responses for client errors (4xx).\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n            - required: [\"500\"]\n\n  response-description-required:\n    description: All response objects must have a description.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].responses[*]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  # Schema Rules\n  schema-type-required:\n    description: All schema objects must define a type.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  schema-description-required:\n    description: All schemas in components must have a description.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-property-description:\n    description: Schema properties should have descriptions for better developer experience.\n    severity: hint\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\S+\"\n\n  # Security\
  \ Rules\n  security-schemes-defined:\n    description: API must define security schemes if authentication is required.\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  # GET Method Rules\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # Vert.x-Specific Rules\n  vertx-health-check-status-enum:\n    description: Health check status fields should use UP or DOWN values.\n    severity: hint\n    given: \"$.components.schemas[?(@.title =~ /.*[Hh]ealth.*/)]..properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  vertx-async-operations-documented:\n    description: Async operations should document their callback or event bus behavior.\n    severity: hint\n    given: \"$.paths[*][post,put,patch].responses[202]\"\n    then:\n      field: description\n\
  \      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vert-x/refs/heads/main/rules/vert-x-spectral-rules.yml
tags:
- Event-Driven
- Frameworks
- Java
- JVM
- Microservices
- Polyglot
- Reactive
- Eclipse Foundation
- Open Source
- Spectral
- Linting
- API Governance
---
