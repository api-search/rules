---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Rollbar REST API
  slug: rollbar-rest-api
  spec_type: OpenAPI
  url: https://explorer.docs.rollbar.com/
- filename: rollbar-deployment-api-openapi.yml
  format: yaml
  label: Rollbar Deployment API
  slug: rollbar-deployment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-deployment-api-openapi.yml
- filename: rollbar-metrics-api-openapi.yml
  format: yaml
  label: Rollbar Metrics API
  slug: rollbar-metrics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-metrics-api-openapi.yml
- filename: rollbar-rql-api-openapi.yml
  format: yaml
  label: Rollbar RQL API
  slug: rollbar-rql-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-rql-api-openapi.yml
- filename: rollbar-webhooks-asyncapi.yml
  format: yaml
  label: Rollbar Webhooks
  slug: rollbar-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/asyncapi/rollbar-webhooks-asyncapi.yml
categories:
- rollbar
description: Spectral linting rules defining API design standards and conventions for Rollbar.
layout: rules
name: Rollbar API Rules
provider_name: Rollbar
provider_slug: rollbar
rule_count: 10
rules:
- description: All Rollbar API operations must reference the accessToken security scheme
  given: $.paths[*][get,post,put,patch,delete]
  name: rollbar-has-access-token-security
  severity: error
- description: Rollbar operationIds use camelCase naming
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: rollbar-operation-id-camel-case
  severity: warn
- description: All Rollbar API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: rollbar-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: rollbar-summary-title-case
  severity: warn
- description: Rollbar path segments must use lowercase kebab-case
  given: $.paths[*]~
  name: rollbar-consistent-path-structure
  severity: warn
- description: All operations should reference defined tags
  given: $.paths[*][get,post,put,patch,delete]
  name: rollbar-tags-defined
  severity: warn
- description: Successful responses should include a schema
  given: $.paths[*][get,post,put,patch,delete].responses[?(@property >= '200' && @property < '300')]
  name: rollbar-success-response-schema
  severity: warn
- description: Operations should document standard error responses
  given: $.paths[*][get,post,put,patch,delete]
  name: rollbar-error-responses-defined
  severity: info
- description: Request bodies must specify application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: rollbar-request-body-content-type
  severity: error
- description: API info section must include contact and terms
  given: $.info
  name: rollbar-info-complete
  severity: warn
rules_file: rules/rollbar-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/rules/rollbar-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 6
slug: rollbar-rules
source_filename: rollbar-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Rollbar API uses X-Rollbar-Access-Token header authentication\n  rollbar-has-access-token-security:\n    description: All Rollbar API operations must reference the accessToken security scheme\n    message: \"Operation must include the accessToken security scheme (X-Rollbar-Access-Token header)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - function: schema\n        functionOptions:\n          schema:\n            type: object\n            anyOf:\n              - required: [security]\n\n  # Operation IDs must be camelCase\n  rollbar-operation-id-camel-case:\n    description: Rollbar operationIds use camelCase naming\n    message: \"OperationId '{{value}}' should be in camelCase format\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations\
  \ must have summaries\n  rollbar-operation-summary-required:\n    description: All Rollbar API operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case\n  rollbar-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Rollbar paths use trailing slashes on collection endpoints\n  rollbar-consistent-path-structure:\n    description: Rollbar path segments must use lowercase kebab-case\n    message: \"Path segment should be lowercase\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n   \
  \     match: \"^(/[a-z0-9_/{}:.-]+)$\"\n\n  # Tags must be defined\n  rollbar-tags-defined:\n    description: All operations should reference defined tags\n    message: \"Operation should reference at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Response schemas should be defined\n  rollbar-success-response-schema:\n    description: Successful responses should include a schema\n    message: \"2xx response should include a content schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[?(@property >= '200' && @property < '300')]\"\n    then:\n      field: content\n      function: truthy\n\n  # Error responses should use standard codes\n  rollbar-error-responses-defined:\n    description: Operations should document standard error responses\n    message: \"Consider documenting 401 and 429 error responses for Rollbar API compliance\"\n    severity: info\n\
  \    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"429\"]\n\n  # Request bodies must have content type\n  rollbar-request-body-content-type:\n    description: Request bodies must specify application/json content type\n    message: \"Request body should use application/json content type\"\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"application/json\"]\n\n  # Info section must be complete\n  rollbar-info-complete:\n    description: API info section must include contact and terms\n    message: \"API info should include contact URL and termsOfService\"\n    severity: warn\n    given: \"$.info\"\
  \n    then:\n      - field: contact\n        function: truthy\n      - field: termsOfService\n        function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/rules/rollbar-rules.yml
tags:
- Error Tracking
- Monitoring
- Debugging
- DevOps
- Application Performance
- Spectral
- Linting
- API Governance
---
