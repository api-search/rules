---
api_specs:
- filename: thought-industries-openapi.yml
  format: yaml
  label: Thought Industries REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thought-industries/refs/heads/main/openapi/thought-industries-openapi.yml
categories:
- thought
description: Spectral linting rules defining API design standards and conventions for Thought Industries.
layout: rules
name: Thought Industries API Rules
provider_name: Thought Industries
provider_slug: thought-industries
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thought-industries-operation-summary-title-case
  severity: warn
- description: List operations should support page and per_page parameters.
  given: $.paths[*][get]
  name: thought-industries-pagination-params
  severity: warn
- description: API key authentication must be documented via X-API-Key header or apiKey query.
  given: $.components.securitySchemes
  name: thought-industries-auth-header-documented
  severity: error
- description: POST/PUT operations must use application/json content type.
  given: $.paths[*][post,put].requestBody.content
  name: thought-industries-request-body-json
  severity: error
- description: Successful responses should wrap data in a data property.
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: thought-industries-response-data-wrapper
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,delete]
  name: thought-industries-tag-defined
  severity: error
- description: Collection paths should use plural resource names.
  given: $.paths
  name: thought-industries-path-resource-plural
  severity: warn
- description: Operation IDs must use camelCase.
  given: $.paths[*][*].operationId
  name: thought-industries-operation-id-camel-case
  severity: warn
rules_file: rules/thought-industries-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thought-industries/refs/heads/main/rules/thought-industries-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: thought-industries-rules
source_filename: thought-industries-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Thought Industries API-specific Spectral rules\n\n  thought-industries-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ -][A-Z0-9][a-z0-9]*)*)$\"\n\n  thought-industries-pagination-params:\n    description: List operations should support page and per_page parameters.\n    message: \"GET list operations should support page and per_page query parameters.\"\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            operationId:\n              pattern: \"^list\"\n\n  thought-industries-auth-header-documented:\n    description: API key authentication must be documented via X-API-Key\
  \ header or apiKey query.\n    message: \"Operations must reference either ApiKeyHeader or ApiKeyQuery security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  thought-industries-request-body-json:\n    description: POST/PUT operations must use application/json content type.\n    message: \"POST/PUT request bodies must use application/json.\"\n    severity: error\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  thought-industries-response-data-wrapper:\n    description: Successful responses should wrap data in a data property.\n    message: \"Responses should use a data wrapper property following Thought Industries conventions.\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      field: data\n      function: truthy\n\n  thought-industries-tag-defined:\n    description:\
  \ All operations must have at least one tag.\n    message: \"Operations must have at least one tag for categorization.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  thought-industries-path-resource-plural:\n    description: Collection paths should use plural resource names.\n    message: \"Collection path segments should use plural nouns (e.g., /users, /courses).\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: truthy\n\n  thought-industries-operation-id-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thought-industries/refs/heads/main/rules/thought-industries-rules.yml
tags:
- Education
- Learning
- LMS
- LXP
- E-Learning
- Training
- Spectral
- Linting
- API Governance
---
