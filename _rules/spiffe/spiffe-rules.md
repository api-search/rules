---
api_specs:
- filename: spiffe-workload-asyncapi.yml
  format: yaml
  label: SPIFFE Workload API
  slug: spiffe-workload-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/spiffe/refs/heads/main/asyncapi/spiffe-workload-asyncapi.yml
- filename: spiffe-federation-openapi.yml
  format: yaml
  label: SPIFFE Federation API
  slug: spiffe-federation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spiffe/refs/heads/main/openapi/spiffe-federation-openapi.yml
categories:
- spiffe
description: Spectral linting rules defining API design standards and conventions for SPIFFE.
layout: rules
name: SPIFFE API Rules
provider_name: SPIFFE
provider_slug: spiffe
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spiffe-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spiffe-tags-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spiffe-operation-id
  severity: error
- description: SPIFFE endpoints must use the /spiffe/v1/ prefix
  given: $.paths[*]~
  name: spiffe-spiffe-path-versioned
  severity: error
- description: SPIFFE endpoints must return application/json
  given: $.paths[*].get.responses.200.content
  name: spiffe-response-content-type
  severity: error
- description: Trust bundle response must include required SPIFFE fields
  given: $.components.schemas.TrustBundle.required
  name: spiffe-trust-bundle-schema
  severity: error
- description: SPIFFE bundle endpoint must be publicly accessible (no auth)
  given: $.paths./spiffe/v1/bundle.get
  name: spiffe-no-auth-on-bundle-endpoint
  severity: warn
rules_file: rules/spiffe-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spiffe/refs/heads/main/rules/spiffe-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 3
slug: spiffe-rules
source_filename: spiffe-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spiffe-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spiffe-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spiffe-operation-id:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spiffe-spiffe-path-versioned:\n\
  \    description: SPIFFE endpoints must use the /spiffe/v1/ prefix\n    message: SPIFFE bundle endpoint paths should use /spiffe/v1/ prefix per the specification\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/spiffe/v[0-9]+\"\n\n  spiffe-response-content-type:\n    description: SPIFFE endpoints must return application/json\n    message: SPIFFE bundle endpoint must return application/json content type\n    severity: error\n    given: \"$.paths[*].get.responses.200.content\"\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  spiffe-trust-bundle-schema:\n    description: Trust bundle response must include required SPIFFE fields\n    message: Trust bundle response must include keys, spiffe_refresh_hint, and spiffe_sequence\n    severity: error\n    given: \"$.components.schemas.TrustBundle.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n        \
  \  type: array\n          contains:\n            type: string\n            enum: [keys, spiffe_refresh_hint, spiffe_sequence]\n\n  spiffe-no-auth-on-bundle-endpoint:\n    description: SPIFFE bundle endpoint must be publicly accessible (no auth)\n    message: The SPIFFE trust bundle endpoint should not require authentication per the specification\n    severity: warn\n    given: \"$.paths./spiffe/v1/bundle.get\"\n    then:\n      field: security\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spiffe/refs/heads/main/rules/spiffe-rules.yml
tags:
- Authentication
- Cloud Native
- Graduated
- Identity
- Security
- Zero Trust
- Spectral
- Linting
- API Governance
---
