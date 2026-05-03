---
api_specs:
- filename: Benefits.json
  format: json
  label: Workday Benefits API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Benefits/v40.2/Benefits.json
categories:
- wdben
description: Spectral linting rules defining API design standards and conventions for Workday Benefits.
layout: rules
name: Workday Benefits API Rules
provider_name: Workday Benefits
provider_slug: workday-benefits
rule_count: 36
rules:
- description: ''
  given: $.info
  name: wdben-info-contact
  severity: warn
- description: ''
  given: $.info.version
  name: wdben-info-version
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: wdben-operation-summary-workday-prefix
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdben-parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdben-parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*].get.responses
  name: wdben-response-200-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdben-response-401-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdben-response-403-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdben-schema-title-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdben-schema-description-required
  severity: warn
- description: ''
  given: $.components.schemas[*].properties[*]
  name: wdben-schema-properties-description
  severity: info
- description: ''
  given: $.components
  name: wdben-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-operation-security-required
  severity: warn
- description: ''
  given: $.components.securitySchemes.oauth2
  name: wdben-oauth2-flows-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdben-microcks-operation-extension
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]
  name: wdben-microcks-example-default
  severity: info
- description: ''
  given: $.paths
  name: wdben-path-camel-case
  severity: info
- description: ''
  given: $.components.schemas
  name: wdben-schema-pascal-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: wdben-operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]
  name: wdben-pagination-limit-param
  severity: info
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]
  name: wdben-pagination-offset-param
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema
  name: wdben-response-schema-ref
  severity: warn
- description: ''
  given: $.servers[*].url
  name: wdben-server-tenant-variable
  severity: warn
- description: ''
  given: $.components.responses[*].content.application/json.schema
  name: wdben-error-response-schema
  severity: info
- description: ''
  given: $.tags
  name: wdben-tags-global-defined
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json
  name: wdben-examples-provided
  severity: info
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdben-request-body-description
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdben-request-body-required-flag
  severity: warn
- description: ''
  given: $.components.schemas[?(@.title =~ /Enrollment/)].properties
  name: wdben-enrollment-effective-date
  severity: info
- description: ''
  given: $.components.schemas.Dependent.properties
  name: wdben-dependent-dob-required
  severity: info
- description: ''
  given: $.components.schemas.BenefitPlan.properties.status
  name: wdben-benefit-plan-status-enum
  severity: warn
- description: ''
  given: $.components.schemas[*].properties.coverageLevel
  name: wdben-coverage-level-enum
  severity: info
rules_file: rules/workday-benefits-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-benefits/refs/heads/main/rules/workday-benefits-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 11
  warn: 19
slug: workday-benefits-spectral-rules
source_filename: workday-benefits-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # ─── Info ───────────────────────────────────────────────────────────────────\n  wdben-info-contact:\n    message: \"Info object must include a contact with name and url.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      - field: contact.name\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  wdben-info-version:\n    message: \"API version must follow Workday vN format.\"\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+(\\\\.[0-9]+)?$\"\n\n  # ─── Operations ─────────────────────────────────────────────────────────────\n  wdben-operation-id-required:\n    message: \"Every operation must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wdben-operation-summary-required:\n    message: \"Every operation must have a summary.\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  wdben-operation-summary-workday-prefix:\n    message: \"Operation summary must start with 'Workday '.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday \"\n\n  wdben-operation-description-required:\n    message: \"Every operation must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  wdben-operation-tags-required:\n    message: \"Every operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # ─── Parameters ─────────────────────────────────────────────────────────────\n  wdben-parameter-description-required:\n\
  \    message: \"Every parameter must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdben-parameter-schema-required:\n    message: \"Every parameter must have a schema.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # ─── Responses ───────────────────────────────────────────────────────────────\n  wdben-response-200-required:\n    message: \"GET operations must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  wdben-response-401-required:\n    message: \"Operations must define a 401 unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  wdben-response-403-required:\n\
  \    message: \"Operations must define a 403 forbidden response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"403\"\n      function: truthy\n\n  # ─── Schemas ─────────────────────────────────────────────────────────────────\n  wdben-schema-title-required:\n    message: \"Every schema in components must have a title.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\n  wdben-schema-description-required:\n    message: \"Every schema in components must have a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdben-schema-properties-description:\n    message: \"Schema properties should have descriptions.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # ─── Security ────────────────────────────────────────────────────────────────\n\
  \  wdben-security-schemes-defined:\n    message: \"API must define security schemes in components.\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  wdben-operation-security-required:\n    message: \"All operations must have security defined.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  wdben-oauth2-flows-defined:\n    message: \"OAuth2 security scheme must define flows.\"\n    severity: error\n    given: \"$.components.securitySchemes.oauth2\"\n    then:\n      field: flows\n      function: truthy\n\n  # ─── Microcks Extensions ────────────────────────────────────────────────────\n  wdben-microcks-operation-extension:\n    message: \"Operations should include x-microcks-operation extension for mock configuration.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n\
  \      function: truthy\n\n  wdben-microcks-example-default:\n    message: \"Response examples should include x-microcks-default: true for the primary example.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]\"\n    then:\n      field: x-microcks-default\n      function: truthy\n\n  # ─── Naming Conventions ─────────────────────────────────────────────────────\n  wdben-path-camel-case:\n    message: \"Path segments should use camelCase per Workday conventions.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-zA-Z0-9/{}_.]*$\"\n\n  wdben-schema-pascal-case:\n    message: \"Schema names in components must use PascalCase.\"\n    severity: warn\n    given: \"$.components.schemas\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  wdben-operation-id-camel-case:\n    message: \"Operation IDs should\
  \ use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ─── Workday-Specific Patterns ───────────────────────────────────────────────\n  wdben-pagination-limit-param:\n    message: \"List operations should support a limit parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdben-pagination-offset-param:\n    message: \"List operations should support an offset parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdben-response-schema-ref:\n    message: \"Success responses\
  \ should reference a defined schema component.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  wdben-server-tenant-variable:\n    message: \"Server URL should include a {tenant} variable for multi-tenant support.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  wdben-error-response-schema:\n    message: \"Error responses should reference the ErrorResponse schema.\"\n    severity: info\n    given: \"$.components.responses[*].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  # ─── Documentation ───────────────────────────────────────────────────────────\n  wdben-tags-global-defined:\n    message: \"Tags used in operations should be defined at the global level.\"\n    severity: warn\n    given: \"\
  $.tags\"\n    then:\n      field: description\n      function: truthy\n\n  wdben-examples-provided:\n    message: \"Responses should include examples for documentation.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json\"\n    then:\n      field: examples\n      function: truthy\n\n  wdben-request-body-description:\n    message: \"Request bodies should include a description.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  wdben-request-body-required-flag:\n    message: \"Request bodies should explicitly declare if they are required.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: required\n      function: defined\n\n  # ─── Benefits-Specific Rules ─────────────────────────────────────────────────\n  wdben-enrollment-effective-date:\n    message: \"Enrollment resources should\
  \ include effectiveDate field.\"\n    severity: info\n    given: \"$.components.schemas[?(@.title =~ /Enrollment/)].properties\"\n    then:\n      field: effectiveDate\n      function: defined\n\n  wdben-dependent-dob-required:\n    message: \"Dependent schemas should include dateOfBirth field.\"\n    severity: info\n    given: \"$.components.schemas.Dependent.properties\"\n    then:\n      field: dateOfBirth\n      function: defined\n\n  wdben-benefit-plan-status-enum:\n    message: \"BenefitPlan status field should use defined enum values.\"\n    severity: warn\n    given: \"$.components.schemas.BenefitPlan.properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  wdben-coverage-level-enum:\n    message: \"Coverage level fields should use defined enum values.\"\n    severity: info\n    given: \"$.components.schemas[*].properties.coverageLevel\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-benefits/refs/heads/main/rules/workday-benefits-spectral-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
