---
api_specs:
- filename: axway-amplify-platform-openapi-original.json
  format: json
  label: Axway Amplify Platform API
  slug: axway-amplify-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/axway/refs/heads/main/openapi/axway-amplify-platform-openapi-original.json
categories:
- info
- microcks
- naming
- operations
- parameters
- paths
- request
- responses
- schemas
- security
description: Spectral linting rules defining API design standards and conventions for Axway.
layout: rules
name: Axway API Rules
provider_name: Axway
provider_slug: axway
rule_count: 32
rules:
- description: API spec must have a non-empty info.title
  given: $.info
  name: info-title-required
  severity: error
- description: API spec must have an info.description
  given: $.info
  name: info-description-required
  severity: error
- description: Info version should follow semantic versioning
  given: $.info.version
  name: info-version-semver
  severity: warn
- description: API spec should include contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Path segments must be lowercase
  given: $.paths
  name: paths-lowercase
  severity: error
- description: Paths must not end with a trailing slash
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: Path segments should use lowercase or snake_case (Axway convention)
  given: $.paths
  name: paths-kebab-or-lower
  severity: warn
- description: Paths should not include file extensions
  given: $.paths
  name: paths-no-file-extensions
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operations-operation-id-required
  severity: error
- description: operationId should use underscore convention (resource_action)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operations-operation-id-underscore
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operations-summary-required
  severity: error
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operations-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operations-tags-required
  severity: error
- description: Tags should be lowercase (Axway convention)
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: operations-tags-lowercase
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameters-description-required
  severity: warn
- description: Every parameter must have a schema with type
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameters-schema-required
  severity: error
- description: Parameter names should use camelCase or snake_case
  given: $.paths[*][get,post,put,patch,delete].parameters[*].name
  name: parameters-camel-case
  severity: info
- description: Every operation must define a success response (2xx)
  given: $.paths[*][get,post,put,patch,delete].responses
  name: responses-success-required
  severity: error
- description: Operations with security should define a 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: responses-error-401
  severity: warn
- description: POST/PUT operations should define a 400 response
  given: $.paths[*][post,put].responses
  name: responses-error-400
  severity: info
- description: Every schema must declare a type
  given: $.components.schemas[*]
  name: schemas-type-required
  severity: error
- description: Schemas should have a description
  given: $.components.schemas[*]
  name: schemas-description-recommended
  severity: info
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schemas-properties-description
  severity: info
- description: Object schemas should explicitly set additionalProperties
  given: $.components.schemas[?(@.type=='object')]
  name: schemas-no-additional-properties-unset
  severity: info
- description: API must define at least one security scheme
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Bearer security schemes should specify bearerFormat
  given: $.components.securitySchemes[?(@.scheme=='bearer')]
  name: security-bearer-format
  severity: info
- description: OAuth2 schemes should define scopes
  given: $.components.securitySchemes[?(@.type=='oauth2')].flows[*]
  name: security-oauth2-scopes
  severity: warn
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json
  severity: warn
- description: Request body JSON content must have a schema
  given: $.paths[*][post,put,patch].requestBody.content.application/json
  name: request-body-schema
  severity: error
- description: Schema names should use PascalCase
  given: $.components.schemas
  name: naming-schema-pascal-case
  severity: warn
- description: Operations should include x-microcks-operation for mock compatibility
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
- description: Success responses should include named examples for Microcks
  given: $.paths[*][get,post,put,patch,delete].responses.200.content.application/json
  name: microcks-response-examples
  severity: info
rules_file: rules/axway-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/axway/refs/heads/main/rules/axway-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 8
  warn: 12
slug: axway-spectral-rules
source_filename: axway-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # ── Info ──────────────────────────────────────────────────────────────\n  info-title-required:\n    description: API spec must have a non-empty info.title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: API spec must have an info.description\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-semver:\n    description: Info version should follow semantic versioning\n    severity: warn\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[0-9]+\\\\.[0-9]+\\\\.[0-9]+\"\n\n  info-contact-required:\n    description: API spec should include contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # ── Paths ─────────────────────────────────────────────────────────────\n  paths-lowercase:\n\
  \    description: Path segments must be lowercase\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9_{}.-]+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-kebab-or-lower:\n    description: Path segments should use lowercase or snake_case (Axway convention)\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9_{}-]+$\"\n\n  paths-no-file-extensions:\n    description: Paths should not include file extensions\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\.(json|xml|yaml|html)$\"\n\n  # ── Operations ────────────────────────────────────────────────────────\n  operations-operation-id-required:\n\
  \    description: Every operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operations-operation-id-underscore:\n    description: operationId should use underscore convention (resource_action)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z]+_[a-zA-Z]+$\"\n\n  operations-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  operations-description-required:\n    description: Every operation must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  operations-tags-required:\n    description:\
  \ Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  operations-tags-lowercase:\n    description: Tags should be lowercase (Axway convention)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_-]*$\"\n\n  # ── Parameters ────────────────────────────────────────────────────────\n  parameters-description-required:\n    description: Every parameter must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameters-schema-required:\n    description: Every parameter must have a schema with type\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function:\
  \ truthy\n\n  parameters-camel-case:\n    description: Parameter names should use camelCase or snake_case\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9_]*$\"\n\n  # ── Responses ─────────────────────────────────────────────────────────\n  responses-success-required:\n    description: Every operation must define a success response (2xx)\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required: [\"204\"]\n\n  responses-error-401:\n    description: Operations with security should define a 401 response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field:\
  \ \"401\"\n      function: truthy\n\n  responses-error-400:\n    description: POST/PUT operations should define a 400 response\n    severity: info\n    given: \"$.paths[*][post,put].responses\"\n    then:\n      field: \"400\"\n      function: truthy\n\n  # ── Schemas ───────────────────────────────────────────────────────────\n  schemas-type-required:\n    description: Every schema must declare a type\n    severity: error\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  schemas-description-recommended:\n    description: Schemas should have a description\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schemas-properties-description:\n    description: Schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schemas-no-additional-properties-unset:\n\
  \    description: Object schemas should explicitly set additionalProperties\n    severity: info\n    given: \"$.components.schemas[?(@.type=='object')]\"\n    then:\n      field: additionalProperties\n      function: defined\n\n  # ── Security ──────────────────────────────────────────────────────────\n  security-schemes-defined:\n    description: API must define at least one security scheme\n    severity: error\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-bearer-format:\n    description: Bearer security schemes should specify bearerFormat\n    severity: info\n    given: \"$.components.securitySchemes[?(@.scheme=='bearer')]\"\n    then:\n      field: bearerFormat\n      function: truthy\n\n  security-oauth2-scopes:\n    description: OAuth2 schemes should define scopes\n    severity: warn\n    given: \"$.components.securitySchemes[?(@.type=='oauth2')].flows[*]\"\n    then:\n      field: scopes\n      function: truthy\n\n  # ── Request\
  \ Bodies ────────────────────────────────────────────────────\n  request-body-json:\n    description: Request bodies should use application/json content type\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  request-body-schema:\n    description: Request body JSON content must have a schema\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  # ── Naming Conventions ────────────────────────────────────────────────\n  naming-schema-pascal-case:\n    description: Schema names should use PascalCase\n    severity: warn\n    given: $.components.schemas\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  # ── Microcks ──────────────────────────────────────────────────────────\n  microcks-operation-extension:\n    description: Operations\
  \ should include x-microcks-operation for mock compatibility\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  microcks-response-examples:\n    description: Success responses should include named examples for Microcks\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses.200.content.application/json\"\n    then:\n      field: examples\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/axway/refs/heads/main/rules/axway-spectral-rules.yml
tags:
- API Management
- Enterprise
- Integration
- Security
- Spectral
- Linting
- API Governance
---
