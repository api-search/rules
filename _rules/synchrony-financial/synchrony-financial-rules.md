---
api_specs:
- filename: synchrony-financial-credit-authorization-openapi.yml
  format: yaml
  label: Synchrony Credit Authorization API
  slug: credit-authorization
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synchrony-financial/refs/heads/main/openapi/synchrony-financial-credit-authorization-openapi.yml
- filename: synchrony-financial-quickscreen-apply-openapi.yml
  format: yaml
  label: Synchrony Quickscreen Apply API
  slug: quickscreen-apply
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synchrony-financial/refs/heads/main/openapi/synchrony-financial-quickscreen-apply-openapi.yml
categories:
- credit
- operation
- paths
- post
- response
description: Spectral linting rules defining API design standards and conventions for Synchrony Financial.
layout: rules
name: Synchrony Financial API Rules
provider_name: Synchrony Financial
provider_slug: synchrony-financial
rule_count: 11
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All paths must include a version prefix (e.g., /v1/).
  given: $.paths
  name: paths-versioned
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: Credit authorization operations must include merchantId in the request body.
  given: $.paths['/v1/authorizations/*'].post.requestBody.content['application/json'].schema.properties
  name: credit-auth-merchant-id
  severity: warn
- description: Response schemas should use $ref references for reusability.
  given: $.paths[*][*].responses[*].content['application/json'].schema
  name: response-schema-ref
  severity: info
- description: POST operations should include 400 or 422 error responses.
  given: $.paths[*].post.responses
  name: post-error-response
  severity: warn
- description: All operations should declare security requirements.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-security
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths
  name: paths-kebab-case
  severity: warn
rules_file: rules/synchrony-financial-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/synchrony-financial/refs/heads/main/rules/synchrony-financial-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 7
slug: synchrony-financial-rules
source_filename: synchrony-financial-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Require operationId on all operations\n  operation-operationId:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require summary on all operations\n  operation-summary:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Enforce Title Case on operation summaries\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # All paths must start with /v1/\n  paths-versioned:\n    description: All paths must include a version prefix (e.g.,\
  \ /v1/).\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+/\"\n\n  # Require tags on all operations\n  operation-tags:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Require description on all operations\n  operation-description:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Credit authorization specific: POST body must have merchantId\n  credit-auth-merchant-id:\n    description: Credit authorization operations must include merchantId in the request body.\n    severity: warn\n    given: \"$.paths['/v1/authorizations/*'].post.requestBody.content['application/json'].schema.properties\"\n    then:\n      field:\
  \ merchantId\n      function: truthy\n\n  # Response schemas should be referenced (not inline)\n  response-schema-ref:\n    description: Response schemas should use $ref references for reusability.\n    severity: info\n    given: \"$.paths[*][*].responses[*].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required:\n                - \"$ref\"\n            - type: object\n\n  # Require 400 or 422 responses on POST operations\n  post-error-response:\n    description: POST operations should include 400 or 422 error responses.\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"422\"]\n\n  # Require security on all operations\n  operation-security:\n    description: All operations should declare security requirements.\n    severity:\
  \ warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # Paths must use kebab-case\n  paths-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/synchrony-financial/refs/heads/main/rules/synchrony-financial-rules.yml
tags:
- Financial Services
- Credit
- Payments
- Consumer Finance
- Retail Finance
- Spectral
- Linting
- API Governance
---
