---
api_specs:
- filename: tazama-transaction-monitoring-service-openapi.yml
  format: yaml
  label: Tazama Transaction Monitoring Service API
  slug: transaction-monitoring-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tazama/refs/heads/main/openapi/tazama-transaction-monitoring-service-openapi.yml
categories:
- tazama
description: Spectral linting rules defining API design standards and conventions for Tazama.
layout: rules
name: Tazama API Rules
provider_name: Tazama
provider_slug: tazama
rule_count: 10
rules:
- description: ISO 20022 transaction paths should follow the /v1/evaluate/iso20022/{messageType} pattern
  given: $.paths[*]~
  name: tazama-iso20022-paths
  severity: warn
- description: All operations must have operationId defined
  given: $.paths[*][get,post,put,delete,patch]
  name: tazama-operation-ids-required
  severity: error
- description: operationId values should use camelCase convention consistent with Tazama TypeScript codebase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: tazama-operation-ids-kebab-case
  severity: warn
- description: POST endpoints accepting transaction data should require application/json content type
  given: $.paths[*].post.requestBody.content
  name: tazama-request-body-json
  severity: warn
- description: All operations should define a 200 or 201 success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: tazama-response-200-defined
  severity: error
- description: All operations should define 400 and 500 error responses
  given: $.paths[*][post].responses
  name: tazama-error-responses
  severity: warn
- description: API info should include contact information
  given: $.info
  name: tazama-info-contact
  severity: warn
- description: All operations should be tagged for proper grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: tazama-tags-defined
  severity: warn
- description: Operations should have descriptions explaining their purpose
  given: $.paths[*][get,post,put,delete,patch]
  name: tazama-description-required
  severity: warn
- description: All schemas in components should be named using PascalCase
  given: $.components.schemas[*]~
  name: tazama-schemas-named
  severity: warn
rules_file: rules/tazama-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tazama/refs/heads/main/rules/tazama-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 8
slug: tazama-rules
source_filename: tazama-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tazama-iso20022-paths:\n    description: ISO 20022 transaction paths should follow the /v1/evaluate/iso20022/{messageType} pattern\n    message: \"Path '{{property}}' should follow /v1/evaluate/iso20022/{messageType} convention for ISO 20022 endpoints\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v1/evaluate/iso20022/|/|/health)\"\n\n  tazama-operation-ids-required:\n    description: All operations must have operationId defined\n    message: \"Operation at '{{path}}' is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: defined\n\n  tazama-operation-ids-kebab-case:\n    description: operationId values should use camelCase convention consistent with Tazama TypeScript codebase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n \
  \   given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tazama-request-body-json:\n    description: POST endpoints accepting transaction data should require application/json content type\n    message: \"POST operation at '{{path}}' should require application/json request body\"\n    severity: warn\n    given: \"$.paths[*].post.requestBody.content\"\n    then:\n      field: \"application/json\"\n      function: defined\n\n  tazama-response-200-defined:\n    description: All operations should define a 200 or 201 success response\n    message: \"Operation at '{{path}}' is missing a success response (200 or 201)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  tazama-error-responses:\n\
  \    description: All operations should define 400 and 500 error responses\n    message: \"Operation is missing error response definitions\"\n    severity: warn\n    given: \"$.paths[*][post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - \"400\"\n            - \"500\"\n\n  tazama-info-contact:\n    description: API info should include contact information\n    message: \"API info is missing contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  tazama-tags-defined:\n    description: All operations should be tagged for proper grouping\n    message: \"Operation at '{{path}}' is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: defined\n\n  tazama-description-required:\n    description: Operations should have descriptions explaining their purpose\n    message:\
  \ \"Operation at '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: defined\n\n  tazama-schemas-named:\n    description: All schemas in components should be named using PascalCase\n    message: \"Schema '{{property}}' should use PascalCase naming\"\n    severity: warn\n    given: \"$.components.schemas[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tazama/refs/heads/main/rules/tazama-rules.yml
tags:
- Financial Technology
- Fraud Detection
- Anti-Money Laundering
- Linux Foundation
- Open Source
- Transaction Monitoring
- ISO 20022
- Real Time
- Spectral
- Linting
- API Governance
---
