---
api_specs:
- filename: Compensation.yaml
  format: yaml
  label: Workday Advanced Compensation API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Compensation/v41.1/Compensation.yaml
categories:
- wdcomp
description: Spectral linting rules defining API design standards and conventions for Workday Advanced Compensation.
layout: rules
name: Workday Advanced Compensation API Rules
provider_name: Workday Advanced Compensation
provider_slug: workday-advanced-compensation
rule_count: 35
rules:
- description: ''
  given: $.info
  name: wdcomp-info-contact
  severity: warn
- description: ''
  given: $.info.version
  name: wdcomp-info-version
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: wdcomp-operation-summary-workday-prefix
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdcomp-parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdcomp-parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*].get.responses
  name: wdcomp-response-200-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdcomp-response-401-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdcomp-response-403-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdcomp-schema-title-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdcomp-schema-description-required
  severity: warn
- description: ''
  given: $.components.schemas[*].properties[*]
  name: wdcomp-schema-properties-description
  severity: info
- description: ''
  given: $.components
  name: wdcomp-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-operation-security-required
  severity: warn
- description: ''
  given: $.components.securitySchemes.oauth2
  name: wdcomp-oauth2-flows-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdcomp-microcks-operation-extension
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]
  name: wdcomp-microcks-example-default
  severity: info
- description: ''
  given: $.paths
  name: wdcomp-path-kebab-case
  severity: info
- description: ''
  given: $.components.schemas
  name: wdcomp-schema-pascal-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: wdcomp-operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]
  name: wdcomp-pagination-limit-param
  severity: info
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]
  name: wdcomp-pagination-offset-param
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema
  name: wdcomp-response-schema-ref
  severity: warn
- description: ''
  given: $.servers[*].url
  name: wdcomp-server-tenant-variable
  severity: warn
- description: ''
  given: $.components.responses[*].content.application/json.schema
  name: wdcomp-error-response-schema
  severity: info
- description: ''
  given: $.tags
  name: wdcomp-tags-global-defined
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json
  name: wdcomp-examples-provided
  severity: info
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdcomp-request-body-description
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdcomp-request-body-required-flag
  severity: warn
- description: ''
  given: $.components.schemas[*].properties
  name: wdcomp-compensation-effective-date
  severity: info
- description: ''
  given: $.components.schemas[?(@.properties.basePay || @.properties.budgetAmount || @.properties.minimumPay)].properties
  name: wdcomp-compensation-currency-field
  severity: info
- description: ''
  given: $.components.schemas[*].properties.status
  name: wdcomp-compensation-status-enum
  severity: warn
rules_file: rules/workday-advanced-compensation-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-advanced-compensation/refs/heads/main/rules/workday-advanced-compensation-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 10
  warn: 19
slug: workday-advanced-compensation-spectral-rules
source_filename: workday-advanced-compensation-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # ─── Info ───────────────────────────────────────────────────────────────────\n  wdcomp-info-contact:\n    message: \"Info object must include a contact with name and url.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      - field: contact.name\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  wdcomp-info-version:\n    message: \"API version must follow Workday vN format.\"\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+(\\\\.[0-9]+)?$\"\n\n  # ─── Operations ─────────────────────────────────────────────────────────────\n  wdcomp-operation-id-required:\n    message: \"Every operation must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wdcomp-operation-summary-required:\n    message: \"Every operation must have a summary.\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  wdcomp-operation-summary-workday-prefix:\n    message: \"Operation summary must start with 'Workday '.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday \"\n\n  wdcomp-operation-description-required:\n    message: \"Every operation must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  wdcomp-operation-tags-required:\n    message: \"Every operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # ─── Parameters ─────────────────────────────────────────────────────────────\n  wdcomp-parameter-description-required:\n\
  \    message: \"Every parameter must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdcomp-parameter-schema-required:\n    message: \"Every parameter must have a schema.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # ─── Responses ───────────────────────────────────────────────────────────────\n  wdcomp-response-200-required:\n    message: \"GET operations must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  wdcomp-response-401-required:\n    message: \"Operations must define a 401 unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  wdcomp-response-403-required:\n\
  \    message: \"Operations must define a 403 forbidden response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"403\"\n      function: truthy\n\n  # ─── Schemas ─────────────────────────────────────────────────────────────────\n  wdcomp-schema-title-required:\n    message: \"Every schema in components must have a title.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\n  wdcomp-schema-description-required:\n    message: \"Every schema in components must have a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdcomp-schema-properties-description:\n    message: \"Schema properties should have descriptions.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # ─── Security ────────────────────────────────────────────────────────────────\n\
  \  wdcomp-security-schemes-defined:\n    message: \"API must define security schemes in components.\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  wdcomp-operation-security-required:\n    message: \"All operations must have security defined.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  wdcomp-oauth2-flows-defined:\n    message: \"OAuth2 security scheme must define flows.\"\n    severity: error\n    given: \"$.components.securitySchemes.oauth2\"\n    then:\n      field: flows\n      function: truthy\n\n  # ─── Microcks Extensions ────────────────────────────────────────────────────\n  wdcomp-microcks-operation-extension:\n    message: \"Operations should include x-microcks-operation extension for mock configuration.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n\
  \      function: truthy\n\n  wdcomp-microcks-example-default:\n    message: \"Response examples should include x-microcks-default: true for the primary example.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]\"\n    then:\n      field: x-microcks-default\n      function: truthy\n\n  # ─── Naming Conventions ─────────────────────────────────────────────────────\n  wdcomp-path-kebab-case:\n    message: \"Path segments should use camelCase per Workday conventions.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-zA-Z0-9/{}_.]*$\"\n\n  wdcomp-schema-pascal-case:\n    message: \"Schema names in components must use PascalCase.\"\n    severity: warn\n    given: \"$.components.schemas\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  wdcomp-operation-id-camel-case:\n    message: \"Operation IDs should\
  \ use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ─── Workday-Specific Patterns ───────────────────────────────────────────────\n  wdcomp-pagination-limit-param:\n    message: \"List operations should support a limit parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdcomp-pagination-offset-param:\n    message: \"List operations should support an offset parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdcomp-response-schema-ref:\n    message: \"Success\
  \ responses should reference a defined schema component.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  wdcomp-server-tenant-variable:\n    message: \"Server URL should include a {tenant} variable for multi-tenant support.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  wdcomp-error-response-schema:\n    message: \"Error responses should reference the ErrorResponse schema.\"\n    severity: info\n    given: \"$.components.responses[*].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  # ─── Documentation ───────────────────────────────────────────────────────────\n  wdcomp-tags-global-defined:\n    message: \"Tags used in operations should be defined at the global level.\"\n    severity: warn\n\
  \    given: \"$.tags\"\n    then:\n      field: description\n      function: truthy\n\n  wdcomp-examples-provided:\n    message: \"Responses should include examples for documentation.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json\"\n    then:\n      field: examples\n      function: truthy\n\n  wdcomp-request-body-description:\n    message: \"Request bodies should include a description.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  wdcomp-request-body-required-flag:\n    message: \"Request bodies should explicitly declare if they are required.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: required\n      function: defined\n\n  # ─── Compensation-Specific Rules ─────────────────────────────────────────────\n  wdcomp-compensation-effective-date:\n    message: \"Compensation\
  \ resources should include effectiveDate field.\"\n    severity: info\n    given: \"$.components.schemas[*].properties\"\n    then:\n      field: effectiveDate\n      function: defined\n\n  wdcomp-compensation-currency-field:\n    message: \"Monetary schemas should include a currency field.\"\n    severity: info\n    given: \"$.components.schemas[?(@.properties.basePay || @.properties.budgetAmount || @.properties.minimumPay)].properties\"\n    then:\n      field: currency\n      function: defined\n\n  wdcomp-compensation-status-enum:\n    message: \"Status fields should use defined enum values.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-advanced-compensation/refs/heads/main/rules/workday-advanced-compensation-spectral-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
