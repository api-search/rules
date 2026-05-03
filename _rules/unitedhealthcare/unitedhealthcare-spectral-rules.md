---
api_specs:
- filename: unitedhealthcare-provider-api-openapi.yml
  format: yaml
  label: UnitedHealthcare Provider API
  slug: provider-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unitedhealthcare/refs/heads/main/openapi/unitedhealthcare-provider-api-openapi.yml
- filename: unitedhealthcare-interoperability-api-openapi.yml
  format: yaml
  label: UnitedHealthcare Interoperability API
  slug: interoperability-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unitedhealthcare/refs/heads/main/openapi/unitedhealthcare-interoperability-api-openapi.yml
categories:
- fhir
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- post
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for UnitedHealthcare.
layout: rules
name: UnitedHealthcare API Rules
provider_name: UnitedHealthcare
provider_slug: unitedhealthcare
rule_count: 27
rules:
- description: API title must be present.
  given: $.info.title
  name: info-title-required
  severity: error
- description: UnitedHealthcare API titles should start with "UnitedHealthcare".
  given: $.info.title
  name: info-title-uhc-prefix
  severity: warn
- description: API description must be present and meaningful.
  given: $.info.description
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info.version
  name: info-version-required
  severity: error
- description: APIs should use OpenAPI 3.x.
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
- description: UnitedHealthcare API servers should use uhcprovider.com or uhc.com domain.
  given: $.servers[*].url
  name: servers-uhc-domain
  severity: warn
- description: Path segments should use kebab-case.
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with UnitedHealthcare.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-prefix
  severity: info
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
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All operations should define a 401 Unauthorized response.
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
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: GET operations must not have a request body.
  given: $.paths[*].get.requestBody
  name: get-no-request-body
  severity: error
- description: POST operations that create resources should return 201 Created.
  given: $.paths[*].post.responses
  name: post-created-response
  severity: info
- description: FHIR schemas should include a resourceType property.
  given: $.components.schemas[?(@.title =~ /^UnitedHealthcare FHIR/)].properties
  name: fhir-resource-type-required
  severity: info
- description: Operations should include x-microcks-operation for mock compatibility.
  given: $.paths[*][get,post,put,delete,patch]
  name: microcks-operation-present
  severity: info
rules_file: rules/unitedhealthcare-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unitedhealthcare/refs/heads/main/rules/unitedhealthcare-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 4
  warn: 10
slug: unitedhealthcare-spectral-rules
source_filename: unitedhealthcare-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present.\n    severity: error\n    given: \"$.info.title\"\n    then:\n      function: truthy\n\n  info-title-uhc-prefix:\n    description: UnitedHealthcare API titles should start with \"UnitedHealthcare\".\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^UnitedHealthcare\"\n\n  info-description-required:\n    description: API description must be present and meaningful.\n    severity: warn\n    given: \"$.info.description\"\n    then:\n      function: minLength\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: \"$.info.version\"\n    then:\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version:\n    description: APIs should use OpenAPI 3.x.\n    severity: warn\n    given: \"$.openapi\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers array must be defined.\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: truthy\n\n  servers-https-only:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-uhc-domain:\n    description: UnitedHealthcare API servers should use uhcprovider.com or uhc.com domain.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(uhcprovider\\\\.com|uhc\\\\.com)\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments should use kebab-case.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}./]+)+$\"\
  \n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-prefix:\n    description: Operation summaries should start with UnitedHealthcare.\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^UnitedHealthcare\"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n\
  \    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: OperationIds should use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].tags\"\n    then:\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: Every parameter must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: Every parameter must\
  \ have a schema.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must define at least one 2xx response.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: truthy\n\n  response-401-required:\n    description: All operations should define a 401 Unauthorized response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-description-required:\n    description: Top-level schemas should have a description.\n\
  \    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get.requestBody\"\n    then:\n      function: falsy\n\n  post-created-response:\n    description: POST operations that create resources should return 201 Created.\n    severity: info\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  # HEALTHCARE SPECIFIC\n  fhir-resource-type-required:\n    description: FHIR schemas should include a resourceType property.\n    severity: info\n    given: \"$.components.schemas[?(@.title =~ /^UnitedHealthcare FHIR/)].properties\"\
  \n    then:\n      field: resourceType\n      function: truthy\n\n  # GENERAL QUALITY\n  microcks-operation-present:\n    description: Operations should include x-microcks-operation for mock compatibility.\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unitedhealthcare/refs/heads/main/rules/unitedhealthcare-spectral-rules.yml
tags:
- Health Insurance
- Healthcare
- FHIR
- Claims
- Eligibility
- Spectral
- Linting
- API Governance
---
