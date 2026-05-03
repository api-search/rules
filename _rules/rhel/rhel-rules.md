---
api_specs:
- filename: openapi.json
  format: json
  label: Red Hat Subscription Management API
  slug: subscription-management-api
  spec_type: OpenAPI
  url: https://api.access.redhat.com/management/v1/openapi.json
- filename: openapi.json
  format: json
  label: Red Hat Insights API
  slug: insights-api
  spec_type: OpenAPI
  url: https://cloud.redhat.com/api/insights/v1/openapi.json
- filename: rhel-security-data-openapi.yml
  format: yaml
  label: Red Hat Security Data API
  slug: security-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rhel/refs/heads/main/openapi/rhel-security-data-openapi.yml
- filename: openapi.json
  format: json
  label: Red Hat Insights Compliance API
  slug: compliance-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/compliance/v2/openapi.json
- filename: openapi.json
  format: json
  label: Red Hat Insights Vulnerability API
  slug: vulnerability-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/vulnerability/v1/openapi.json
- filename: openapi.json
  format: json
  label: Red Hat Insights Patch API
  slug: patch-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/patch/v3/openapi.json
- filename: openapi.json
  format: json
  label: Red Hat Insights Host Inventory API
  slug: inventory-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/inventory/v1/openapi.json
- filename: openapi.json
  format: json
  label: Red Hat Insights Remediations API
  slug: remediations-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/remediations/v1/openapi.json
categories:
- rhel
description: Spectral linting rules defining API design standards and conventions for Red Hat Enterprise Linux.
layout: rules
name: Red Hat Enterprise Linux API Rules
provider_name: Red Hat Enterprise Linux
provider_slug: rhel
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: rhel-operation-summary-title-case
  severity: warn
- description: Operation IDs should be camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: rhel-operation-id-kebab-case
  severity: warn
- description: Tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: rhel-tags-must-be-title-case
  severity: warn
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: rhel-must-have-security
  severity: error
- description: GET operations must return a 200 response
  given: $.paths[*].get
  name: rhel-responses-must-include-200
  severity: error
- description: API responses must use application/json content type
  given: $.paths[*][get].responses[200].content
  name: rhel-json-response-content-type
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: rhel-parameters-must-have-description
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]
  name: rhel-path-params-must-be-required
  severity: error
- description: All servers must use HTTPS
  given: $.servers[*].url
  name: rhel-server-must-be-https
  severity: error
rules_file: rules/rhel-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rhel/refs/heads/main/rules/rhel-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: rhel-rules
source_filename: rhel-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rhel-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]* )*[A-Z][a-z]*$\"\n\n  rhel-operation-id-kebab-case:\n    description: Operation IDs should be camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rhel-tags-must-be-title-case:\n    description: Tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  rhel-must-have-security:\n    description: All operations must define security requirements\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: security\n      function: defined\n\n  rhel-responses-must-include-200:\n    description: GET operations must return a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  rhel-json-response-content-type:\n    description: API responses must use application/json content type\n    severity: warn\n    given: \"$.paths[*][get].responses[200].content\"\n    then:\n      field: application/json\n      function: defined\n\n  rhel-parameters-must-have-description:\n    description: All parameters must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: defined\n\n  rhel-path-params-must-be-required:\n    description: Path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]\"\n    then:\n     \
  \ field: required\n      function: truthy\n\n  rhel-server-must-be-https:\n    description: All servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rhel/refs/heads/main/rules/rhel-rules.yml
tags:
- Automation
- Compliance
- Enterprise
- Linux
- Operating System
- Red Hat
- RHEL
- Security
- Subscription Management
- Vulnerability Management
- Spectral
- Linting
- API Governance
---
