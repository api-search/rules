---
api_specs:
- filename: sap-integration-suite-cloud-integration-openapi.yml
  format: yaml
  label: SAP Cloud Integration API
  slug: sap-cloud-integration
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-integration-suite/refs/heads/main/openapi/sap-integration-suite-cloud-integration-openapi.yml
- filename: sap-integration-suite-api-management-openapi.yml
  format: yaml
  label: SAP API Management API
  slug: sap-api-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-integration-suite/refs/heads/main/openapi/sap-integration-suite-api-management-openapi.yml
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP Integration Suite.
layout: rules
name: SAP Integration Suite API Rules
provider_name: SAP Integration Suite
provider_slug: sap-integration-suite
rule_count: 11
rules:
- description: SAP OData entity set names must use PascalCase
  given: $.paths[*]~
  name: sap-odata-entity-pascal-case
  severity: warn
- description: OData key predicates must use parenthetical notation
  given: $.paths[*]~
  name: sap-odata-key-notation
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: sap-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-operation-summary-required
  severity: error
- description: OData filter parameters must be named $filter
  given: $.paths[*][get].parameters[*]
  name: sap-odata-filter-parameter
  severity: warn
- description: OData pagination parameters must use $top and $skip
  given: $.paths[*][get].parameters[*]
  name: sap-odata-pagination-parameters
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: sap-schema-description
  severity: warn
- description: SAP APIs should use OAuth2 authentication
  given: $.components.securitySchemes
  name: sap-oauth2-security-defined
  severity: warn
- description: Tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: sap-tags-title-case
  severity: warn
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-operation-description
  severity: warn
- description: Secured operations should define 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sap-401-response-defined
  severity: warn
rules_file: rules/sap-integration-suite-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-integration-suite/refs/heads/main/rules/sap-integration-suite-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 10
slug: sap-integration-suite-rules
source_filename: sap-integration-suite-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SAP OData entity naming conventions\n  sap-odata-entity-pascal-case:\n    description: SAP OData entity set names must use PascalCase\n    message: Entity set path segment '{{value}}' should use PascalCase (e.g., IntegrationPackages not integration-packages)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[A-Z][a-zA-Z]*|/\\\\{[a-z][a-zA-Z]*\\\\})+$\"\n\n  # OData key notation in paths\n  sap-odata-key-notation:\n    description: OData key predicates must use parenthetical notation\n    message: OData key segments should use parenthetical notation (e.g., /Entities('{Id}'))\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^.*$\"\n\n  # SAP operation IDs must be camelCase\n  sap-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: OperationId '{{value}}'\
  \ should use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have summaries\n  sap-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # OData filter parameter should use $filter naming\n  sap-odata-filter-parameter:\n    description: OData filter parameters must be named $filter\n    message: Filter parameters in OData APIs should be named '$filter'\n    severity: warn\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                pattern: \"filter\"\n          then:\n            properties:\n \
  \             name:\n                enum:\n                  - \"$filter\"\n\n  # OData pagination parameters\n  sap-odata-pagination-parameters:\n    description: OData pagination parameters must use $top and $skip\n    message: Pagination parameter should be named '$top' or '$skip'\n    severity: warn\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                pattern: \"^(top|skip)$\"\n          then:\n            properties:\n              name:\n                enum:\n                  - \"$top\"\n                  - \"$skip\"\n\n  # All schemas should have descriptions\n  sap-schema-description:\n    description: Schema properties should have descriptions\n    message: Property '{{path}}' is missing a description\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\
  \n  # OAuth2 security must be defined\n  sap-oauth2-security-defined:\n    description: SAP APIs should use OAuth2 authentication\n    message: OAuth2 security scheme should be defined for SAP APIs\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: oauth2\n      function: truthy\n\n  # Tags must use Title Case\n  sap-tags-title-case:\n    description: Tags must use Title Case\n    message: Tag '{{value}}' should use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # Operations must have descriptions\n  sap-operation-description:\n    description: Operations should have descriptions\n    message: Operation is missing a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Response 401 must be defined for secured\
  \ operations\n  sap-401-response-defined:\n    description: Secured operations should define 401 response\n    message: Operation is missing a 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-integration-suite/refs/heads/main/rules/sap-integration-suite-rules.yml
tags:
- API Management
- Cloud Integration
- Enterprise Integration
- Event Mesh
- iPaaS
- SAP
- SAP BTP
- Spectral
- Linting
- API Governance
---
