---
api_specs:
- filename: salesforce-automation-flow-openapi.yml
  format: yaml
  label: Salesforce Flow Automation API
  slug: salesforce-flow-automation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-automation-system/refs/heads/main/openapi/salesforce-automation-flow-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Automation System.
layout: rules
name: Salesforce Automation System API Rules
provider_name: Salesforce Automation System
provider_slug: salesforce-automation-system
rule_count: 8
rules:
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: salesforce-operation-id-required
  severity: error
- description: Operation summaries should use Title Case.
  given: $.paths[*][*].summary
  name: salesforce-summary-title-case
  severity: warn
- description: Salesforce APIs must declare OAuth2 or Bearer security.
  given: $.components.securitySchemes
  name: salesforce-oauth2-required
  severity: error
- description: All operations must define a 200 or 201 response.
  given: $.paths[*][*].responses
  name: salesforce-response-200-defined
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: salesforce-tags-required
  severity: warn
- description: Server URL should include a version identifier.
  given: $.servers[*].url
  name: salesforce-versioned-server
  severity: warn
- description: Operations should define 401 and 403 error responses.
  given: $.paths[*][*].responses
  name: salesforce-error-responses
  severity: warn
- description: Request bodies must use application/json.
  given: $.paths[*][*].requestBody.content
  name: salesforce-content-type-json
  severity: error
rules_file: rules/salesforce-automation-system-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-automation-system/refs/heads/main/rules/salesforce-automation-system-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: salesforce-automation-system-rules
source_filename: salesforce-automation-system-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  salesforce-operation-id-required:\n    description: All operations must have an operationId.\n    message: \"Operation is missing operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  salesforce-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-oauth2-required:\n    description: Salesforce APIs must declare OAuth2 or Bearer security.\n    message: \"Salesforce API must declare OAuth2 authentication.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"oauth2\"]\n            - required:\
  \ [\"bearerAuth\"]\n\n  salesforce-response-200-defined:\n    description: All operations must define a 200 or 201 response.\n    message: \"Operation must define a success response.\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  salesforce-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  salesforce-versioned-server:\n    description: Server URL should include a version identifier.\n    message: \"Server URL should include API version (e.g., /v59.0).\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]\"\n\n  salesforce-error-responses:\n\
  \    description: Operations should define 401 and 403 error responses.\n    message: \"Operations should define authentication/authorization error responses.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\", \"403\"]\n\n  salesforce-content-type-json:\n    description: Request bodies must use application/json.\n    message: \"Request body must declare application/json content type.\"\n    severity: error\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"application/json\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-automation-system/refs/heads/main/rules/salesforce-automation-system-rules.yml
tags:
- Approval Process
- Automation
- CRM
- Flow
- Process Builder
- Salesforce
- Workflow
- Spectral
- Linting
- API Governance
---
