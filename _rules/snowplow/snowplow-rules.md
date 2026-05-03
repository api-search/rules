---
api_specs:
- filename: snowplow-console-api-openapi.yml
  format: yaml
  label: Snowplow Console API
  slug: snowplow-console-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snowplow/refs/heads/main/openapi/snowplow-console-api-openapi.yml
categories:
- snowplow
description: Spectral linting rules defining API design standards and conventions for Snowplow.
layout: rules
name: Snowplow API Rules
provider_name: Snowplow
provider_slug: snowplow
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: snowplow-operation-id-camel-case
  severity: warn
- description: All Snowplow Console API paths should be scoped to an organization
  given: $.paths[*]~
  name: snowplow-org-scoped-paths
  severity: warn
- description: Operations must define security (JWT bearer token)
  given: $.paths[*][get,post,put,delete,patch]
  name: snowplow-security-defined
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: snowplow-operation-tag
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: snowplow-operation-summary
  severity: warn
- description: Operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: snowplow-operation-description
  severity: info
- description: All path parameters must have required=true
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: snowplow-path-params-required
  severity: error
- description: Snowplow Console API uses version suffixes in resource paths (v1, v2)
  given: $.paths[*]~
  name: snowplow-path-version-suffix
  severity: info
rules_file: rules/snowplow-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/snowplow/refs/heads/main/rules/snowplow-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: snowplow-rules
source_filename: snowplow-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation ID naming\n  snowplow-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Organization scoped paths\n  snowplow-org-scoped-paths:\n    description: All Snowplow Console API paths should be scoped to an organization\n    message: \"Path should include organizationId scope\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/organizations/.*\"\n\n  # Auth requirements\n  snowplow-security-defined:\n    description: Operations must define security (JWT bearer token)\n    message: \"Operation must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n\
  \      field: security\n      function: defined\n\n  # Tag requirements\n  snowplow-operation-tag:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summary in Title Case\n  snowplow-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Description requirements\n  snowplow-operation-description:\n    description: Operations should have a description\n    message: \"Operation should have a description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  # Path parameter defined\n  snowplow-path-params-required:\n\
  \    description: All path parameters must have required=true\n    message: \"Path parameters must be required\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  # Version suffix in paths\n  snowplow-path-version-suffix:\n    description: Snowplow Console API uses version suffixes in resource paths (v1, v2)\n    message: \"Resource paths should include version suffix\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/v[0-9]+(/|$)\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/snowplow/refs/heads/main/rules/snowplow-rules.yml
tags:
- Analytics Platform
- Behavioral Data
- Data Collection
- Data Engineering
- Data Pipeline
- Event Tracking
- Open Source
- Spectral
- Linting
- API Governance
---
