---
api_specs:
- filename: wellcare-fhir-patient-access-api-openapi.yml
  format: yaml
  label: WellCare FHIR Patient Access API
  slug: fhir-patient-access-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wellcare-health-plans/refs/heads/main/openapi/wellcare-fhir-patient-access-api-openapi.yml
- filename: wellcare-fhir-provider-directory-api-openapi.yml
  format: yaml
  label: WellCare FHIR Provider Directory API
  slug: fhir-provider-directory-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wellcare-health-plans/refs/heads/main/openapi/wellcare-fhir-provider-directory-api-openapi.yml
categories:
- fhir
- operation
- response
description: Spectral linting rules defining API design standards and conventions for wellcare-health-plans.
layout: rules
name: wellcare-health-plans API Rules
provider_name: wellcare-health-plans
provider_slug: wellcare-health-plans
rule_count: 9
rules:
- description: All FHIR endpoints must use /fhir/r4/ path prefix.
  given: $.paths[*]~
  name: fhir-r4-path-prefix
  severity: error
- description: FHIR resource segments must use UpperCamelCase (e.g., Patient, ExplanationOfBenefit).
  given: $.paths[*]~
  name: fhir-resource-title-case
  severity: warn
- description: All FHIR operations must define security scopes.
  given: $.paths[*][get,post,put,delete]
  name: fhir-operation-security
  severity: error
- description: FHIR responses should return application/fhir+json content type.
  given: $.paths[*][get].responses[200].content
  name: fhir-accept-header
  severity: warn
- description: Operation IDs must use lowerCamelCase.
  given: $.paths[*][*].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: FHIR search operations on clinical resources must support the patient parameter.
  given: $.paths[/fhir/r4/Coverage,/fhir/r4/ExplanationOfBenefit,/fhir/r4/Condition,/fhir/r4/Observation,/fhir/r4/MedicationRequest,/fhir/r4/Immunization,/fhir/r4/Encounter].get.parameters[*]
  name: fhir-search-patient-param
  severity: hint
- description: Secured operations must define a 401 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
rules_file: rules/wellcare-health-plans-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wellcare-health-plans/refs/heads/main/rules/wellcare-health-plans-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 5
slug: wellcare-health-plans-rules
source_filename: wellcare-health-plans-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # FHIR API path conventions\n  fhir-r4-path-prefix:\n    description: All FHIR endpoints must use /fhir/r4/ path prefix.\n    message: \"FHIR endpoint '{{property}}' must start with /fhir/r4/.\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/fhir/r4/\"\n\n  # FHIR resource naming\n  fhir-resource-title-case:\n    description: FHIR resource segments must use UpperCamelCase (e.g., Patient, ExplanationOfBenefit).\n    message: \"FHIR resource name in path '{{value}}' must use UpperCamelCase.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/fhir/r4/[A-Z][A-Za-z]+\"\n\n  # SMART on FHIR scopes\n  fhir-operation-security:\n    description: All FHIR operations must define security scopes.\n    message: \"FHIR operation '{{path}}' must define security requirements.\"\n    severity: error\n\
  \    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # HL7 FHIR content type\n  fhir-accept-header:\n    description: FHIR responses should return application/fhir+json content type.\n    message: \"FHIR response should use 'application/fhir+json' content type.\"\n    severity: warn\n    given: \"$.paths[*][get].responses[200].content\"\n    then:\n      field: \"application/fhir+json\"\n      function: defined\n\n  # Operation IDs - camelCase required\n  operation-id-camel-case:\n    description: Operation IDs must use lowerCamelCase.\n    message: \"Operation ID '{{value}}' must use lowerCamelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries required\n  operation-summary-required:\n    description: All operations must have a summary.\n    message: \"Operation at '{{path}}' must have a summary.\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Tags required on operations\n  operation-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # FHIR search: patient parameter required\n  fhir-search-patient-param:\n    description: FHIR search operations on clinical resources must support the patient parameter.\n    message: \"FHIR search operation should support 'patient' query parameter.\"\n    severity: hint\n    given: \"$.paths[/fhir/r4/Coverage,/fhir/r4/ExplanationOfBenefit,/fhir/r4/Condition,/fhir/r4/Observation,/fhir/r4/MedicationRequest,/fhir/r4/Immunization,/fhir/r4/Encounter].get.parameters[*]\"\n    then:\n      field: name\n      function: enumeration\n     \
  \ functionOptions:\n        values: [patient, _count, _page, service-date, type, category, status, date]\n\n  # 401 responses required on secured operations\n  response-401-required:\n    description: Secured operations must define a 401 response.\n    message: \"Secured operation '{{path}}' must define a 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wellcare-health-plans/refs/heads/main/rules/wellcare-health-plans-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
