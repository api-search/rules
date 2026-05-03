---
api_specs:
- filename: united-airlines-ndc-openapi.yml
  format: yaml
  label: United Airlines NDC API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-airlines/main/openapi/united-airlines-ndc-openapi.yml
categories:
- info
- operation
- parameter
- path
- response
- schema
- servers
- ua
description: Spectral linting rules defining API design standards and conventions for United Airlines.
layout: rules
name: United Airlines API Rules
provider_name: United Airlines
provider_slug: united-airlines
rule_count: 15
rules:
- description: Every operation must have a unique operationId.
  given: $.paths.*[get,post,put,patch,delete,options,head]
  name: operation-operationId
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must include at least one tag.
  given: $.paths.*[get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: Every operation must have a description.
  given: $.paths.*[get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: Path segments must use kebab-case (lowercase with hyphens).
  given: $.paths[*]~
  name: path-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: path-no-trailing-slash
  severity: error
- description: All response status codes must include a description.
  given: $.paths.*[get,post,put,patch,delete].responses.*
  name: response-descriptions
  severity: warn
- description: Every operation must define a security requirement.
  given: $.paths.*[get,post,put,patch,delete]
  name: operation-security-defined
  severity: warn
- description: POST, PUT, and PATCH operations should have a requestBody.
  given: $.paths.*[post,put,patch]
  name: operation-request-body-required
  severity: warn
- description: API info must include contact information.
  given: $.info
  name: info-contact
  severity: warn
- description: All named schemas should have a description.
  given: $.components.schemas.*
  name: schema-description
  severity: info
- description: Operations must define at least one 2xx success response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: operation-success-response
  severity: error
- description: All parameters must have a description.
  given: $.paths.*[get,post,put,patch,delete].parameters.*
  name: parameter-description
  severity: warn
- description: Flight number examples should follow United Airlines UA format (e.g., UA123).
  given: $.components.schemas.FlightSegment.properties.flightNumber.example
  name: ua-flight-number-format
  severity: info
- description: API must define at least one server.
  given: $
  name: servers-defined
  severity: error
rules_file: rules/united-airlines-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-airlines/refs/heads/main/rules/united-airlines-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 9
slug: united-airlines-rules
source_filename: united-airlines-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Require operationId on every operation\n  operation-operationId:\n    description: Every operation must have a unique operationId.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require operation summary in Title Case\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Require tags on every operation\n  operation-tags:\n    description: Every operation must include at least one tag.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Require description on every operation\n\
  \  operation-description:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Paths must use kebab-case\n  path-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens).\n    message: \"Path '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  # Paths must not have a trailing slash\n  path-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  # All response codes must have descriptions\n  response-descriptions:\n    description: All response status codes must include a description.\n    severity: warn\n    given:\
  \ \"$.paths.*[get,post,put,patch,delete].responses.*\"\n    then:\n      field: description\n      function: truthy\n\n  # Require security on every operation\n  operation-security-defined:\n    description: Every operation must define a security requirement.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # POST/PUT/PATCH must have a requestBody\n  operation-request-body-required:\n    description: POST, PUT, and PATCH operations should have a requestBody.\n    severity: warn\n    given: \"$.paths.*[post,put,patch]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # API must have contact information\n  info-contact:\n    description: API info must include contact information.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # All schemas must have a description\n  schema-description:\n    description: All named schemas should\
  \ have a description.\n    severity: info\n    given: \"$.components.schemas.*\"\n    then:\n      field: description\n      function: truthy\n\n  # Require 2xx success response for all operations\n  operation-success-response:\n    description: Operations must define at least one 2xx success response.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  # Parameters must have descriptions\n  parameter-description:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].parameters.*\"\n    then:\n      field: description\n      function: truthy\n\n  # United Airlines: Flight-domain-specific rule — flight numbers must follow UA format\n  ua-flight-number-format:\n    description: Flight number examples should follow United Airlines UA format (e.g., UA123).\n\
  \    message: \"Flight number example '{{value}}' should follow UA### format.\"\n    severity: info\n    given: \"$.components.schemas.FlightSegment.properties.flightNumber.example\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^UA\\\\d+$\"\n\n  # Servers must be defined\n  servers-defined:\n    description: API must define at least one server.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-airlines/refs/heads/main/rules/united-airlines-rules.yml
tags:
- Airlines
- Travel
- Flight Booking
- NDC
- Loyalty
- Fortune 100
- Spectral
- Linting
- API Governance
---
