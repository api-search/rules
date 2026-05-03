---
api_specs:
- filename: tenet-healthcare-fhir-openapi.yml
  format: yaml
  label: Tenet Health Patient Portal API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tenet-healthcare/refs/heads/main/openapi/tenet-healthcare-fhir-openapi.yml
categories:
- tenet
description: Spectral linting rules defining API design standards and conventions for Tenet Healthcare.
layout: rules
name: Tenet Healthcare API Rules
provider_name: Tenet Healthcare
provider_slug: tenet-healthcare
rule_count: 10
rules:
- description: All Tenet FHIR API operations must use SMART on FHIR OAuth 2.0
  given: $.paths[*][get,post,put,patch,delete]
  name: tenet-smart-on-fhir-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: tenet-operation-id-required
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: tenet-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: tenet-summary-title-case
  severity: warn
- description: FHIR API responses should use application/fhir+json content type
  given: $.paths[*][get].responses[200].content
  name: tenet-fhir-content-type
  severity: info
- description: Patient resource paths should define the id path parameter
  given: $.paths[*~'/Patient/{id}'][get].parameters
  name: tenet-patient-id-param
  severity: warn
- description: Search operations should return FHIR Bundle resources
  given: $.paths[*][get].responses[200].content.application/fhir+json.schema
  name: tenet-fhir-bundle-response
  severity: info
- description: API spec must define server URLs
  given: $
  name: tenet-server-urls-required
  severity: error
- description: FHIR API specs should declare the FHIR version
  given: $.info
  name: tenet-fhir-version-info
  severity: info
- description: FHIR operations must define 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: tenet-unauthorized-response
  severity: warn
rules_file: rules/tenet-healthcare-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tenet-healthcare/refs/heads/main/rules/tenet-healthcare-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 5
slug: tenet-healthcare-rules
source_filename: tenet-healthcare-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # FHIR APIs require SMART on FHIR security\n  tenet-smart-on-fhir-required:\n    description: All Tenet FHIR API operations must use SMART on FHIR OAuth 2.0\n    message: \"Operation '{{operationId}}' should reference SMART on FHIR security scheme\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # Enforce operation IDs\n  tenet-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Enforce camelCase operation IDs\n  tenet-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Enforce Title Case summaries\n  tenet-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # FHIR responses should use application/fhir+json\n  tenet-fhir-content-type:\n    description: FHIR API responses should use application/fhir+json content type\n    message: \"FHIR response should use application/fhir+json content type\"\n    severity: info\n    given: \"$.paths[*][get].responses[200].content\"\n    then:\n      field: \"application/fhir+json\"\n      function: truthy\n\n  # Patient paths should have ID parameter\n  tenet-patient-id-param:\n    description: Patient resource paths should define the id path\
  \ parameter\n    message: \"Patient path should define the id parameter\"\n    severity: warn\n    given: \"$.paths[*~'/Patient/{id}'][get].parameters\"\n    then:\n      function: truthy\n\n  # FHIR Bundle responses for search results\n  tenet-fhir-bundle-response:\n    description: Search operations should return FHIR Bundle resources\n    message: \"Search operation should return FHIR Bundle\"\n    severity: info\n    given: \"$.paths[*][get].responses[200].content.application/fhir+json.schema\"\n    then:\n      function: truthy\n\n  # Server URLs required\n  tenet-server-urls-required:\n    description: API spec must define server URLs\n    message: \"API spec is missing server definitions\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  # FHIR version documentation\n  tenet-fhir-version-info:\n    description: FHIR API specs should declare the FHIR version\n    message: \"API spec should document FHIR version in info.version or\
  \ description\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # 401 response required\n  tenet-unauthorized-response:\n    description: FHIR operations must define 401 Unauthorized response\n    message: \"Operation should define 401 Unauthorized response for SMART on FHIR failures\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tenet-healthcare/refs/heads/main/rules/tenet-healthcare-rules.yml
tags:
- Healthcare
- Hospitals
- Ambulatory Surgery Centers
- Revenue Cycle Management
- Fortune 500
- Spectral
- Linting
- API Governance
---
