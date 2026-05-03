---
api_specs:
- filename: tufin-securetrack-openapi.yml
  format: yaml
  label: Tufin SecureTrack API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tufin/refs/heads/main/openapi/tufin-securetrack-openapi.yml
- filename: tufin-securechange-openapi.yml
  format: yaml
  label: Tufin SecureChange API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tufin/refs/heads/main/openapi/tufin-securechange-openapi.yml
categories:
- tufin
description: Spectral linting rules defining API design standards and conventions for Tufin.
layout: rules
name: Tufin API Rules
provider_name: Tufin
provider_slug: tufin
rule_count: 11
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tufin-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: tufin-operation-id-required
  severity: error
- description: Tufin SecureTrack uses HTTP Basic Authentication for all API endpoints. All operations must declare the basicAuth security requirement.
  given: $.paths[*][get,post,put,delete,patch]
  name: tufin-basic-auth-required
  severity: warn
- description: All operations should define a 200 success response
  given: $.paths[*][get,post,put].responses
  name: tufin-200-response-defined
  severity: warn
- description: All operations must be tagged for documentation organization
  given: $.paths[*][get,post,put,delete,patch]
  name: tufin-tag-required
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: tufin-description-required
  severity: warn
- description: Tufin uses integer-based IDs for deviceId, ruleId, ticketId, and taskId. These path parameters must use integer type.
  given: $.paths[*][*].parameters[?(@.in == 'path' && @.name =~ /Id$/)]
  name: tufin-integer-id-path-params
  severity: warn
- description: Tufin SecureTrack API supports both XML and JSON responses. Operations should document the response content type.
  given: $.paths[*][get,post,put].responses.200
  name: tufin-xml-json-response
  severity: info
- description: All parameters should have a description
  given: $.paths[*][*].parameters[*]
  name: tufin-parameter-description
  severity: warn
- description: API must define reusable schemas in components/schemas
  given: $.components
  name: tufin-components-schemas
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: tufin-no-trailing-slashes
  severity: warn
rules_file: rules/tufin-securetrack-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tufin/refs/heads/main/rules/tufin-securetrack-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 8
slug: tufin-securetrack-rules
source_filename: tufin-securetrack-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tufin-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  tufin-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tufin-basic-auth-required:\n    description: >-\n      Tufin SecureTrack uses HTTP Basic Authentication for all API endpoints.\n      All operations must declare the basicAuth security requirement.\n    message: \"Tufin SecureTrack operations must require basicAuth\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n \
  \     field: security\n      function: truthy\n\n  tufin-200-response-defined:\n    description: All operations should define a 200 success response\n    message: \"Operation should define a 200 success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  tufin-tag-required:\n    description: All operations must be tagged for documentation organization\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  tufin-description-required:\n    description: All operations should have a description\n    message: \"Operation should include a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  tufin-integer-id-path-params:\n    description: >-\n      Tufin uses integer-based\
  \ IDs for deviceId, ruleId, ticketId, and taskId.\n      These path parameters must use integer type.\n    message: \"Tufin ID path parameters should use integer type\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path' && @.name =~ /Id$/)]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  tufin-xml-json-response:\n    description: >-\n      Tufin SecureTrack API supports both XML and JSON responses. Operations\n      should document the response content type.\n    message: \"Operations should define response content type\"\n    severity: info\n    given: \"$.paths[*][get,post,put].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  tufin-parameter-description:\n    description: All parameters should have a description\n    message: \"Parameter '{{value}}' should have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n   \
  \ then:\n      field: description\n      function: truthy\n\n  tufin-components-schemas:\n    description: API must define reusable schemas in components/schemas\n    message: \"API should define schemas in components/schemas\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n\n  tufin-no-trailing-slashes:\n    description: Paths must not have trailing slashes\n    message: \"Path '{{property}}' must not end with a trailing slash\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tufin/refs/heads/main/rules/tufin-securetrack-rules.yml
tags:
- Cloud Security
- Compliance
- Firewall Management
- Network Security
- Network Topology
- Policy Orchestration
- Risk Management
- Security Policy Management
- Zero Trust
- Spectral
- Linting
- API Governance
---
