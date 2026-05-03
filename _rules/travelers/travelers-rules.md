---
api_specs:
- filename: travelers-openapi.yml
  format: yaml
  label: Travelers API
  slug: travelers
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/travelers/refs/heads/main/openapi/travelers-openapi.yml
categories:
- travelers
description: Spectral linting rules defining API design standards and conventions for Travelers.
layout: rules
name: Travelers API Rules
provider_name: Travelers
provider_slug: travelers
rule_count: 11
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: travelers-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: travelers-operationid-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: travelers-tags-required
  severity: warn
- description: Insurance API should use OAuth2 authentication
  given: $.components.securitySchemes[*]
  name: travelers-oauth2-required
  severity: warn
- description: GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: travelers-response-200-get
  severity: error
- description: POST operations that create resources should return 201
  given: $.paths[*].post.responses
  name: travelers-response-201-post
  severity: warn
- description: Claim endpoints should use claim_number as path parameter
  given: $.paths['/claims/{claim_number}'][*].parameters[*][?(@.name=='id')]
  name: travelers-claim-number-in-path
  severity: hint
- description: Policy types should be validated against known types
  given: $.components.schemas[*].properties.policy_type
  name: travelers-policy-type-enum
  severity: warn
- description: Date fields should use ISO 8601 date format
  given: $.components.schemas[*].properties[?(@.format=='date')]
  name: travelers-date-format
  severity: warn
- description: Responses should wrap content in a data property
  given: $.components.schemas[?(@property.match(/Response$/))].properties
  name: travelers-data-wrapper
  severity: warn
- description: Monetary amount fields should use number format float
  given: $.components.schemas[*].properties[?(@.property.match(/amount|premium|incurred/i))]
  name: travelers-amount-format
  severity: hint
rules_file: rules/travelers-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/travelers/refs/heads/main/rules/travelers-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 7
slug: travelers-rules
source_filename: travelers-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  travelers-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  travelers-operationid-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  travelers-tags-required:\n    description: All operations must have tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  travelers-oauth2-required:\n    description: Insurance API should use OAuth2 authentication\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - oauth2\n\
  \          - http\n\n  travelers-response-200-get:\n    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  travelers-response-201-post:\n    description: POST operations that create resources should return 201\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  travelers-claim-number-in-path:\n    description: Claim endpoints should use claim_number as path parameter\n    severity: hint\n    given: \"$.paths['/claims/{claim_number}'][*].parameters[*][?(@.name=='id')]\"\n    then:\n      function: falsy\n\n  travelers-policy-type-enum:\n    description: Policy types should be validated against known types\n    severity: warn\n    given: \"$.components.schemas[*].properties.policy_type\"\n    then:\n      field: enum\n      function: truthy\n\n  travelers-date-format:\n    description: Date fields\
  \ should use ISO 8601 date format\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.format=='date')]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n          - date-time\n\n  travelers-data-wrapper:\n    description: Responses should wrap content in a data property\n    severity: warn\n    given: \"$.components.schemas[?(@property.match(/Response$/))].properties\"\n    then:\n      field: data\n      function: truthy\n\n  travelers-amount-format:\n    description: Monetary amount fields should use number format float\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@.property.match(/amount|premium|incurred/i))]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - float\n          - double\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/travelers/refs/heads/main/rules/travelers-rules.yml
tags:
- Insurance
- Property Casualty
- Commercial Insurance
- Claims
- Fintech
- Fortune 500
- Spectral
- Linting
- API Governance
---
