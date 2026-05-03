---
api_specs:
- filename: varian-aria-fhir-openapi.yml
  format: yaml
  label: ARIA FHIR API
  slug: aria-fhir-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/varian-medical-systems/refs/heads/main/openapi/varian-aria-fhir-openapi.yml
categories:
- varian
description: Spectral linting rules defining API design standards and conventions for Varian Medical Systems.
layout: rules
name: Varian Medical Systems API Rules
provider_name: Varian Medical Systems
provider_slug: varian-medical-systems
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: varian-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: varian-operation-ids-present
  severity: error
- description: FHIR APIs should use application/fhir+json content type
  given: $.paths[*][*].responses[*].content
  name: varian-fhir-json-content-type
  severity: warn
- description: Patient-scoped resources should require patient parameter
  given: $.paths[?(!@~property.match('/Patient'))][get].parameters[?(@.name=='patient')]
  name: varian-patient-param-required
  severity: warn
- description: All operations should have tags for grouping
  given: $.paths[*][*]
  name: varian-paths-have-tags
  severity: warn
- description: Path ID parameters must be required
  given: $.paths[*][*].parameters[?(@.name=='id' && @.in=='path')]
  name: varian-id-path-param-required
  severity: error
- description: Search operations should return FHIR Bundle
  given: $.paths[?(!@property.match(/{id}$))][get].responses.200.content.application/fhir+json.schema
  name: varian-fhir-bundle-response
  severity: info
- description: ARIA FHIR API uses SMART on FHIR OAuth2
  given: $.components.securitySchemes
  name: varian-smart-on-fhir-security
  severity: warn
rules_file: rules/varian-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/varian-medical-systems/refs/heads/main/rules/varian-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: varian-rules
source_filename: varian-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  varian-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  varian-operation-ids-present:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  varian-fhir-json-content-type:\n    description: FHIR APIs should use application/fhir+json content type\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"application/fhir\\\\+json\"\n\n  varian-patient-param-required:\n    description: Patient-scoped resources should require patient parameter\n    severity: warn\n    given: \"$.paths[?(!@~property.match('/Patient'))][get].parameters[?(@.name=='patient')]\"\
  \n    then:\n      field: required\n      function: truthy\n\n  varian-paths-have-tags:\n    description: All operations should have tags for grouping\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  varian-id-path-param-required:\n    description: Path ID parameters must be required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name=='id' && @.in=='path')]\"\n    then:\n      field: required\n      function: truthy\n\n  varian-fhir-bundle-response:\n    description: Search operations should return FHIR Bundle\n    severity: info\n    given: \"$.paths[?(!@property.match(/{id}$))][get].responses.200.content.application/fhir+json.schema\"\n    then:\n      field: \"$ref\"\n      function: pattern\n      functionOptions:\n        match: \"Bundle\"\n\n  varian-smart-on-fhir-security:\n    description: ARIA FHIR API uses SMART on FHIR OAuth2\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n\
  \      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/varian-medical-systems/refs/heads/main/rules/varian-rules.yml
tags:
- Healthcare
- Oncology
- Medical Devices
- FHIR
- Radiation Therapy
- Health IT
- Spectral
- Linting
- API Governance
---
