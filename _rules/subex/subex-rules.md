---
api_specs:
- filename: subex-revenue-assurance-openapi.yml
  format: yaml
  label: Subex Revenue Assurance & Fraud Management API
  slug: subex-revenue-assurance-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/subex/refs/heads/main/openapi/subex-revenue-assurance-openapi.yml
categories:
- subex
description: Spectral linting rules defining API design standards and conventions for Subex.
layout: rules
name: Subex API Rules
provider_name: Subex
provider_slug: subex
rule_count: 9
rules:
- description: All Subex API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: subex-operation-id-required
  severity: error
- description: Subex operationIds use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: subex-operation-id-camel-case
  severity: warn
- description: All operations should have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: subex-tags-required
  severity: warn
- description: Subex API uses Bearer token authentication
  given: $.components.securitySchemes
  name: subex-bearer-auth
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: subex-response-200
  severity: warn
- description: List operations should support pagination parameters
  given: $.paths[*].get
  name: subex-pagination-params
  severity: hint
- description: Operations should define a 401 unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: subex-error-401-defined
  severity: hint
- description: API must define servers
  given: $
  name: subex-servers-defined
  severity: error
- description: API should include contact information
  given: $.info
  name: subex-info-contact
  severity: warn
rules_file: rules/subex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/subex/refs/heads/main/rules/subex-rules.yml
severity_counts:
  error: 3
  hint: 2
  info: 0
  warn: 4
slug: subex-rules
source_filename: subex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  subex-operation-id-required:\n    description: All Subex API operations must have an operationId\n    message: \"Operation at '{{path}}' is missing operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  subex-operation-id-camel-case:\n    description: Subex operationIds use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  subex-tags-required:\n    description: All operations should have at least one tag\n    message: \"Operation at '{{path}}' should include tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  subex-bearer-auth:\n    description: Subex\
  \ API uses Bearer token authentication\n    message: \"API must define a BearerAuth security scheme\"\n    given: \"$.components.securitySchemes\"\n    severity: error\n    then:\n      field: BearerAuth\n      function: truthy\n\n  subex-response-200:\n    description: GET operations must define a 200 response\n    message: \"GET operation at '{{path}}' must define a 200 response\"\n    given: \"$.paths[*].get.responses\"\n    severity: warn\n    then:\n      field: \"200\"\n      function: truthy\n\n  subex-pagination-params:\n    description: List operations should support pagination parameters\n    message: \"List operation at '{{path}}' should include page/size parameters\"\n    given: \"$.paths[*].get\"\n    severity: hint\n    then:\n      field: parameters\n      function: truthy\n\n  subex-error-401-defined:\n    description: Operations should define a 401 unauthorized response\n    message: \"Operation should define a 401 response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    severity: hint\n    then:\n      field: \"401\"\n      function: truthy\n\n  subex-servers-defined:\n    description: API must define servers\n    message: \"API must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n\n  subex-info-contact:\n    description: API should include contact information\n    message: \"API info must include contact details\"\n    given: \"$.info\"\n    severity: warn\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/subex/refs/heads/main/rules/subex-rules.yml
tags:
- Telecom
- Revenue Assurance
- Fraud Management
- Analytics
- BSS/OSS
- Spectral
- Linting
- API Governance
---
