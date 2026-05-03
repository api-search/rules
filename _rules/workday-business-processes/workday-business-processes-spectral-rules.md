---
api_specs:
- filename: Business_Process_Service.yaml
  format: yaml
  label: Workday Business Process API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Business_Process_Service/v41.1/Business_Process_Service.yaml
categories:
- wdbp
description: Spectral linting rules defining API design standards and conventions for Workday Business Processes.
layout: rules
name: Workday Business Processes API Rules
provider_name: Workday Business Processes
provider_slug: workday-business-processes
rule_count: 36
rules:
- description: ''
  given: $.info
  name: wdbp-info-contact
  severity: warn
- description: ''
  given: $.info.version
  name: wdbp-info-version
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-operation-id-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].summary
  name: wdbp-operation-summary-workday-prefix
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdbp-parameter-description-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: wdbp-parameter-schema-required
  severity: error
- description: ''
  given: $.paths[*].get.responses
  name: wdbp-response-200-required
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdbp-response-401-required
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wdbp-response-403-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdbp-schema-title-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: wdbp-schema-description-required
  severity: warn
- description: ''
  given: $.components.schemas[*].properties[*]
  name: wdbp-schema-properties-description
  severity: info
- description: ''
  given: $.components
  name: wdbp-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-operation-security-required
  severity: warn
- description: ''
  given: $.components.securitySchemes.oauth2
  name: wdbp-oauth2-flows-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,patch,delete]
  name: wdbp-microcks-operation-extension
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]
  name: wdbp-microcks-example-default
  severity: info
- description: ''
  given: $.paths
  name: wdbp-path-camel-case
  severity: info
- description: ''
  given: $.components.schemas
  name: wdbp-schema-pascal-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: wdbp-operation-id-camel-case
  severity: warn
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]
  name: wdbp-pagination-limit-param
  severity: info
- description: ''
  given: $.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]
  name: wdbp-pagination-offset-param
  severity: info
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema
  name: wdbp-response-schema-ref
  severity: warn
- description: ''
  given: $.servers[*].url
  name: wdbp-server-tenant-variable
  severity: warn
- description: ''
  given: $.components.responses[*].content.application/json.schema
  name: wdbp-error-response-schema
  severity: info
- description: ''
  given: $.tags
  name: wdbp-tags-global-defined
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json
  name: wdbp-examples-provided
  severity: info
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdbp-request-body-description
  severity: warn
- description: ''
  given: $.paths[*][post,put,patch].requestBody
  name: wdbp-request-body-required-flag
  severity: warn
- description: ''
  given: $.components.schemas.ProcessInstance.properties.status
  name: wdbp-process-instance-status-enum
  severity: warn
- description: ''
  given: $.components.schemas.InboxItem.properties.status
  name: wdbp-inbox-item-status-enum
  severity: warn
- description: ''
  given: $.components.schemas.ApprovalRequest
  name: wdbp-approval-request-approver-required
  severity: error
- description: ''
  given: $.components.schemas[*].properties.stepType
  name: wdbp-process-step-type-enum
  severity: warn
rules_file: rules/workday-business-processes-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-business-processes/refs/heads/main/rules/workday-business-processes-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 8
  warn: 21
slug: workday-business-processes-spectral-rules
source_filename: workday-business-processes-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # ─── Info ───────────────────────────────────────────────────────────────────\n  wdbp-info-contact:\n    message: \"Info object must include a contact with name and url.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      - field: contact.name\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  wdbp-info-version:\n    message: \"API version must follow Workday vN format.\"\n    severity: warn\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+(\\\\.[0-9]+)?$\"\n\n  # ─── Operations ─────────────────────────────────────────────────────────────\n  wdbp-operation-id-required:\n    message: \"Every operation must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wdbp-operation-summary-required:\n    message: \"Every operation must have a summary.\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  wdbp-operation-summary-workday-prefix:\n    message: \"Operation summary must start with 'Workday '.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Workday \"\n\n  wdbp-operation-description-required:\n    message: \"Every operation must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  wdbp-operation-tags-required:\n    message: \"Every operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # ─── Parameters ─────────────────────────────────────────────────────────────\n  wdbp-parameter-description-required:\n\
  \    message: \"Every parameter must have a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdbp-parameter-schema-required:\n    message: \"Every parameter must have a schema.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # ─── Responses ───────────────────────────────────────────────────────────────\n  wdbp-response-200-required:\n    message: \"GET operations must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  wdbp-response-401-required:\n    message: \"Operations must define a 401 unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  wdbp-response-403-required:\n\
  \    message: \"Operations must define a 403 forbidden response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"403\"\n      function: truthy\n\n  # ─── Schemas ─────────────────────────────────────────────────────────────────\n  wdbp-schema-title-required:\n    message: \"Every schema in components must have a title.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\n  wdbp-schema-description-required:\n    message: \"Every schema in components must have a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wdbp-schema-properties-description:\n    message: \"Schema properties should have descriptions.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # ─── Security ────────────────────────────────────────────────────────────────\n\
  \  wdbp-security-schemes-defined:\n    message: \"API must define security schemes in components.\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  wdbp-operation-security-required:\n    message: \"All operations must have security defined.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  wdbp-oauth2-flows-defined:\n    message: \"OAuth2 security scheme must define flows.\"\n    severity: error\n    given: \"$.components.securitySchemes.oauth2\"\n    then:\n      field: flows\n      function: truthy\n\n  # ─── Microcks Extensions ────────────────────────────────────────────────────\n  wdbp-microcks-operation-extension:\n    message: \"Operations should include x-microcks-operation extension for mock configuration.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n\
  \      function: truthy\n\n  wdbp-microcks-example-default:\n    message: \"Response examples should include x-microcks-default: true for the primary example.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*].content[*].examples[*]\"\n    then:\n      field: x-microcks-default\n      function: truthy\n\n  # ─── Naming Conventions ─────────────────────────────────────────────────────\n  wdbp-path-camel-case:\n    message: \"Path segments should use camelCase per Workday conventions.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-zA-Z0-9/{}_.]*$\"\n\n  wdbp-schema-pascal-case:\n    message: \"Schema names in components must use PascalCase.\"\n    severity: warn\n    given: \"$.components.schemas\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  wdbp-operation-id-camel-case:\n    message: \"Operation IDs should use\
  \ camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # ─── Workday-Specific Patterns ───────────────────────────────────────────────\n  wdbp-pagination-limit-param:\n    message: \"List operations should support a limit parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'limit')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdbp-pagination-offset-param:\n    message: \"List operations should support an offset parameter.\"\n    severity: info\n    given: \"$.paths[*][?(@property === 'get')].parameters[?(@.name === 'offset')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values: [integer]\n\n  wdbp-response-schema-ref:\n    message: \"Success responses\
  \ should reference a defined schema component.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  wdbp-server-tenant-variable:\n    message: \"Server URL should include a {tenant} variable for multi-tenant support.\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  wdbp-error-response-schema:\n    message: \"Error responses should reference the ErrorResponse schema.\"\n    severity: info\n    given: \"$.components.responses[*].content.application/json.schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  # ─── Documentation ───────────────────────────────────────────────────────────\n  wdbp-tags-global-defined:\n    message: \"Tags used in operations should be defined at the global level.\"\n    severity: warn\n    given: \"$.tags\"\
  \n    then:\n      field: description\n      function: truthy\n\n  wdbp-examples-provided:\n    message: \"Responses should include examples for documentation.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201].content.application/json\"\n    then:\n      field: examples\n      function: truthy\n\n  wdbp-request-body-description:\n    message: \"Request bodies should include a description.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  wdbp-request-body-required-flag:\n    message: \"Request bodies should explicitly declare if they are required.\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: required\n      function: defined\n\n  # ─── Business Process-Specific Rules ─────────────────────────────────────────\n  wdbp-process-instance-status-enum:\n    message: \"ProcessInstance status field should\
  \ use defined enum values.\"\n    severity: warn\n    given: \"$.components.schemas.ProcessInstance.properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  wdbp-inbox-item-status-enum:\n    message: \"InboxItem status field should use defined enum values.\"\n    severity: warn\n    given: \"$.components.schemas.InboxItem.properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  wdbp-approval-request-approver-required:\n    message: \"ApprovalRequest schema must include approverId as required.\"\n    severity: error\n    given: \"$.components.schemas.ApprovalRequest\"\n    then:\n      field: required\n      function: truthy\n\n  wdbp-process-step-type-enum:\n    message: \"Process step type should use defined enum values.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.stepType\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-business-processes/refs/heads/main/rules/workday-business-processes-spectral-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
