---
api_specs:
- filename: vertiv-environet-alert-openapi.yml
  format: yaml
  label: Vertiv Environet Alert REST API
  slug: environet-alert-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vertiv/refs/heads/main/openapi/vertiv-environet-alert-openapi.yml
categories:
- vertiv
description: Spectral linting rules defining API design standards and conventions for Vertiv.
layout: rules
name: Vertiv API Rules
provider_name: Vertiv
provider_slug: vertiv
rule_count: 10
rules:
- description: Operation IDs must use camelCase as per Vertiv API conventions
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: vertiv-operation-ids-kebab-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: vertiv-paths-kebab-case
  severity: warn
- description: All operations (except /auth POST) must declare X-Auth-Token security
  given: $.paths[?(@property != '/auth')][get,put,patch,delete].security
  name: vertiv-require-auth-token-header
  severity: warn
- description: All 200 responses must include a schema definition
  given: $.paths[*][get,post,put,patch,delete].responses['200'].content[*]
  name: vertiv-response-200-must-have-schema
  severity: error
- description: All operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: vertiv-require-operation-tags
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: vertiv-require-operation-description
  severity: warn
- description: All non-2xx responses should reference the shared Error schema
  given: $.paths[*][get,post,put,patch,delete].responses[4*,5*].content['application/json']
  name: vertiv-error-response-schema
  severity: info
- description: Status fields must use Vertiv's standard status enum values
  given: $.components.schemas[*].properties.status.enum
  name: vertiv-status-enum-values
  severity: info
- description: API info must include contact information
  given: $.info
  name: vertiv-require-contact
  severity: info
- description: Server variables must have a description
  given: $.servers[*].variables[*]
  name: vertiv-server-variable-description
  severity: warn
rules_file: rules/vertiv-environet-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vertiv/refs/heads/main/rules/vertiv-environet-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 6
slug: vertiv-environet-rules
source_filename: vertiv-environet-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vertiv-operation-ids-kebab-case:\n    description: Operation IDs must use camelCase as per Vertiv API conventions\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  vertiv-paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{path}}' must use kebab-case segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{][a-z0-9-{}]*)*$\"\n\n  vertiv-require-auth-token-header:\n    description: >-\n      All operations (except /auth POST) must declare X-Auth-Token security\n    message: \"Operation must require session token authentication\"\n    severity: warn\n    given: \"$.paths[?(@property != '/auth')][get,put,patch,delete].security\"\
  \n    then:\n      function: truthy\n\n  vertiv-response-200-must-have-schema:\n    description: All 200 responses must include a schema definition\n    message: \"200 response must include a content schema\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses['200'].content[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  vertiv-require-operation-tags:\n    description: All operations must have at least one tag for grouping\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  vertiv-require-operation-description:\n    description: All operations must have a description\n    message: \"Operation must include a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  vertiv-error-response-schema:\n\
  \    description: >-\n      All non-2xx responses should reference the shared Error schema\n    message: \"Error responses should use the shared Error schema\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[4*,5*].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  vertiv-status-enum-values:\n    description: Status fields must use Vertiv's standard status enum values\n    message: \"Status enum must include standard Vertiv status values\"\n    severity: info\n    given: \"$.components.schemas[*].properties.status.enum\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            enum:\n              - NORMAL\n              - ALARM\n              - WARNING\n\n  vertiv-require-contact:\n    description: API info must include contact information\n    message: \"API info should include contact details\"\n    severity: info\n    given: \"$.info\"\
  \n    then:\n      field: contact\n      function: truthy\n\n  vertiv-server-variable-description:\n    description: Server variables must have a description\n    message: \"Server variable must have a description\"\n    severity: warn\n    given: \"$.servers[*].variables[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vertiv/refs/heads/main/rules/vertiv-environet-rules.yml
tags:
- Critical Infrastructure
- Data Center
- DCIM
- Infrastructure Monitoring
- Power Management
- UPS
- Spectral
- Linting
- API Governance
---
