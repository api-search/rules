---
api_specs:
- filename: salesforcecom-rest-openapi.yml
  format: yaml
  label: Salesforce REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforcecom/refs/heads/main/openapi/salesforcecom-rest-openapi.yml
categories:
- operation
- request
- response
- salesforce
- use
description: Spectral linting rules defining API design standards and conventions for Salesforce.
layout: rules
name: Salesforce API Rules
provider_name: Salesforce
provider_slug: salesforcecom
rule_count: 14
rules:
- description: All Salesforce REST API paths must be versioned under /services/data/v{version}/
  given: $.paths[*]~
  name: salesforce-versioned-path
  severity: warn
- description: Every operation must have an operationId for SDK generation and Postman
  given: $.paths[*][get,post,patch,put,delete]
  name: operation-id-required
  severity: error
- description: Salesforce operationIds should use camelCase
  given: $.paths[*][get,post,patch,put,delete].operationId
  name: salesforce-operation-id-camel-case
  severity: warn
- description: Every operation must be tagged for organization in API docs and Postman
  given: $.paths[*][get,post,patch,put,delete]
  name: operation-tags-required
  severity: warn
- description: Paths containing {sObjectName} must define it as a path parameter
  given: $.paths[*][get,post,patch,put,delete][?(@.parameters)]
  name: salesforce-sobject-parameter
  severity: error
- description: All Salesforce REST API operations must include the version path parameter
  given: $.paths['/services/data/v{version}/**'][get,post,patch,put,delete]
  name: salesforce-version-parameter
  severity: warn
- description: Every operation must define a success response (200, 201, or 204)
  given: $.paths[*][get,post,patch,put,delete].responses
  name: response-success-required
  severity: error
- description: All authenticated Salesforce operations should document 401 Unauthorized
  given: $.paths[*][get,post,patch,put,delete][?(@.security)]
  name: salesforce-401-response
  severity: info
- description: All operations must have a summary for API docs readability
  given: $.paths[*][get,post,patch,put,delete]
  name: operation-summary-required
  severity: warn
- description: Salesforce operation summaries should use Title Case
  given: $.paths[*][get,post,patch,put,delete].summary
  name: salesforce-title-case-summary
  severity: info
- description: Salesforce REST API uses PATCH for partial record updates, not PUT. PUT is used only for upsert operations by external ID.
  given: $.paths[*].put
  name: salesforce-use-patch-for-updates
  severity: info
- description: Request bodies should specify application/json content type
  given: $.paths[*][post,patch,put].requestBody.content
  name: request-body-json
  severity: warn
- description: POST/PATCH operations should document 400 Bad Request for validation errors
  given: $.paths[*][post,patch].responses
  name: salesforce-400-for-mutations
  severity: info
- description: Prefer $ref to component schemas instead of inline schema definitions for consistency and reuse across operations.
  given: $.paths[*][get,post,patch,put,delete].responses[*].content[*].schema
  name: use-schema-refs
  severity: info
rules_file: rules/salesforcecom-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforcecom/refs/heads/main/rules/salesforcecom-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 5
  warn: 6
slug: salesforcecom-rules
source_filename: salesforcecom-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Salesforce REST API uses versioned paths like /services/data/v{version}/...\n  salesforce-versioned-path:\n    description: All Salesforce REST API paths must be versioned under /services/data/v{version}/\n    message: \"Salesforce REST paths should start with /services/data/v{version}/ — found: {{path}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/services/data/v\\\\{version\\\\}/\"\n\n  # All operations must have an operationId\n  operation-id-required:\n    description: Every operation must have an operationId for SDK generation and Postman\n    message: \"Operation at {{path}} is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,patch,put,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationIds must use camelCase (Salesforce convention)\n  salesforce-operation-id-camel-case:\n    description:\
  \ Salesforce operationIds should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,patch,put,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have at least one tag\n  operation-tags-required:\n    description: Every operation must be tagged for organization in API docs and Postman\n    message: \"Operation at {{path}} is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,patch,put,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # sObject paths must include the sObjectName path parameter\n  salesforce-sobject-parameter:\n    description: Paths containing {sObjectName} must define it as a path parameter\n    message: \"Path {{path}} uses {sObjectName} but sObjectName parameter is not defined\"\n    severity: error\n    given: \"$.paths[*][get,post,patch,put,delete][?(@.parameters)]\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  # version path parameter must be in every path operation\n  salesforce-version-parameter:\n    description: All Salesforce REST API operations must include the version path parameter\n    message: \"Operation {{path}} should include the 'version' path parameter\"\n    severity: warn\n    given: \"$.paths['/services/data/v{version}/**'][get,post,patch,put,delete]\"\n    then:\n      field: parameters\n      function: truthy\n\n  # Responses must include at least a 200 or 204 success response\n  response-success-required:\n    description: Every operation must define a success response (200, 201, or 204)\n    message: \"Operation at {{path}} must have a 2xx success response\"\n    severity: error\n    given: \"$.paths[*][get,post,patch,put,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n       \
  \     - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  # 401 Unauthorized response should be on all authenticated operations\n  salesforce-401-response:\n    description: All authenticated Salesforce operations should document 401 Unauthorized\n    message: \"Authenticated operation at {{path}} should document 401 Unauthorized\"\n    severity: info\n    given: \"$.paths[*][get,post,patch,put,delete][?(@.security)]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  # Summary should be present on all operations\n  operation-summary-required:\n    description: All operations must have a summary for API docs readability\n    message: \"Operation {{path}} is missing summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,patch,put,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case (Salesforce convention)\n  salesforce-title-case-summary:\n    description: Salesforce operation\
  \ summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: info\n    given: \"$.paths[*][get,post,patch,put,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # PATCH (not PUT) for updates in Salesforce REST API\n  salesforce-use-patch-for-updates:\n    description: >-\n      Salesforce REST API uses PATCH for partial record updates, not PUT.\n      PUT is used only for upsert operations by external ID.\n    message: \"Consider PATCH instead of PUT for record updates (Salesforce convention)\"\n    severity: info\n    given: \"$.paths[*].put\"\n    then:\n      function: truthy\n\n  # Request body must have content type application/json\n  request-body-json:\n    description: Request bodies should specify application/json content type\n    message: \"Request body at {{path}} should include application/json content type\"\n    severity: warn\n    given: \"$.paths[*][post,patch,put].requestBody.content\"\
  \n    then:\n      field: application/json\n      function: truthy\n\n  # 400 response should be documented for POST/PATCH operations\n  salesforce-400-for-mutations:\n    description: POST/PATCH operations should document 400 Bad Request for validation errors\n    message: \"Mutation operation at {{path}} should document 400 Bad Request\"\n    severity: info\n    given: \"$.paths[*][post,patch].responses\"\n    then:\n      field: '400'\n      function: truthy\n\n  # Schema $ref should be used instead of inline schemas for reusability\n  use-schema-refs:\n    description: >-\n      Prefer $ref to component schemas instead of inline schema definitions\n      for consistency and reuse across operations.\n    message: \"Inline schema at {{path}} — consider using a $ref to components/schemas\"\n    severity: info\n    given: \"$.paths[*][get,post,patch,put,delete].responses[*].content[*].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n\
  \            - required: ['$ref']\n            - type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforcecom/refs/heads/main/rules/salesforcecom-rules.yml
tags:
- CRM
- Cloud
- Sales
- Marketing
- Automation
- AI
- Spectral
- Linting
- API Governance
---
