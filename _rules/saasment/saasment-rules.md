---
api_specs:
- filename: saasment-openapi.yml
  format: yaml
  label: Saasment API
  slug: saasment
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/saasment/refs/heads/main/openapi/saasment-openapi.yml
categories:
- saasment
description: Spectral linting rules defining API design standards and conventions for Saasment.
layout: rules
name: Saasment API Rules
provider_name: Saasment
provider_slug: saasment
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: saasment-operation-summary-title-case
  severity: warn
- description: All endpoints except public must require BearerAuth security
  given: $.paths[*][*]
  name: saasment-security-bearer-required
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: saasment-operation-ids-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: saasment-tags-required
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][get,put,patch].responses
  name: saasment-response-200-defined
  severity: error
- description: Operations should define 401 unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: saasment-error-responses-defined
  severity: warn
- description: List endpoints should support pagination with page and per_page
  given: $.paths[*][get]
  name: saasment-pagination-parameters
  severity: info
- description: Severity fields should use standard enum values
  given: $.components.schemas..properties.severity
  name: saasment-severity-enum
  severity: warn
- description: Resource ID fields should be string type for UUID compatibility
  given: $.components.schemas..properties.id
  name: saasment-resource-ids-as-strings
  severity: info
rules_file: rules/saasment-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/saasment/refs/heads/main/rules/saasment-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: saasment-rules
source_filename: saasment-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  saasment-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*)( [A-Z][a-z]*)*$\"\n\n  saasment-security-bearer-required:\n    description: All endpoints except public must require BearerAuth security\n    message: \"Endpoint must declare security requirements\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: security\n      function: defined\n\n  saasment-operation-ids-kebab-case:\n    description: Operation IDs should use camelCase\n    message: \"Operation ID '{{value}}' should use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  saasment-tags-required:\n\
  \    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  saasment-response-200-defined:\n    description: All operations must define a success response\n    message: \"Operation must define at least a 200 or 201 response\"\n    given: \"$.paths[*][get,put,patch].responses\"\n    severity: error\n    then:\n      field: \"200\"\n      function: defined\n\n  saasment-error-responses-defined:\n    description: Operations should define 401 unauthorized response\n    message: \"Operation should define 401 response for authentication errors\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    severity: warn\n    then:\n      field: \"401\"\n      function: defined\n\n  saasment-pagination-parameters:\n    description: List endpoints should support pagination with page and per_page\n    message: \"List endpoints\
  \ should include page and per_page query parameters\"\n    given: \"$.paths[*][get]\"\n    severity: info\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n\n  saasment-severity-enum:\n    description: Severity fields should use standard enum values\n    message: \"Severity fields should use standard values: critical, high, medium, low, info\"\n    given: \"$.components.schemas..properties.severity\"\n    severity: warn\n    then:\n      field: enum\n      function: defined\n\n  saasment-resource-ids-as-strings:\n    description: Resource ID fields should be string type for UUID compatibility\n    message: \"ID fields should be string type\"\n    given: \"$.components.schemas..properties.id\"\n    severity: info\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/saasment/refs/heads/main/rules/saasment-rules.yml
tags:
- SaaS Security
- SSPM
- Cloud Security
- Cost Optimization
- Compliance
- Misconfigurations
- Spectral
- Linting
- API Governance
---
