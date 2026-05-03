---
api_specs:
- filename: apispec
  format: yaml
  label: USDA FoodData Central API
  slug: fooddata-central-api
  spec_type: OpenAPI
  url: https://fdc.nal.usda.gov/portal-data/external/apispec
- filename: usda-ars-ag-data-commons-openapi.yml
  format: yaml
  label: USDA Ag Data Commons CKAN API
  slug: ag-data-commons-ckan-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/usda-agricultural-research-service-ars-/refs/heads/main/openapi/usda-ars-ag-data-commons-openapi.yml
categories:
- usda
description: Spectral linting rules defining API design standards and conventions for USDA Agricultural Research Service (ARS).
layout: rules
name: USDA Agricultural Research Service (ARS) API Rules
provider_name: USDA Agricultural Research Service (ARS)
provider_slug: usda-agricultural-research-service-ars-
rule_count: 7
rules:
- description: All operations must have a summary
  given: $.paths[*][*]
  name: usda-ars-operation-summary
  severity: error
- description: All operations must have tags
  given: $.paths[*][*]
  name: usda-ars-operation-tags
  severity: warn
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: usda-ars-get-200-response
  severity: error
- description: FoodData Central API requires api_key parameter
  given: $.paths[*].get.parameters[*]
  name: usda-ars-api-key-authentication
  severity: info
- description: Path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: usda-ars-path-params-documented
  severity: warn
- description: APIs should document the CC0 license
  given: $.info
  name: usda-ars-license-info
  severity: info
- description: APIs should have contact information
  given: $.info
  name: usda-ars-contact-info
  severity: warn
rules_file: rules/usda-agricultural-research-service-ars--rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/usda-agricultural-research-service-ars-/refs/heads/main/rules/usda-agricultural-research-service-ars--rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 3
slug: usda-agricultural-research-service-ars--rules
source_filename: usda-agricultural-research-service-ars--rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  usda-ars-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation missing summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  usda-ars-operation-tags:\n    description: All operations must have tags\n    message: \"Operation missing tags\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  usda-ars-get-200-response:\n    description: GET operations must define a 200 response\n    message: \"GET operation missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  usda-ars-api-key-authentication:\n    description: FoodData Central API requires api_key parameter\n    message: \"FDC API endpoints should document api_key query parameter\"\n    severity: info\n    given: \"$.paths[*].get.parameters[*]\"\
  \n    then:\n      function: truthy\n\n  usda-ars-path-params-documented:\n    description: Path parameters must have descriptions\n    message: \"Path parameter missing description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  usda-ars-license-info:\n    description: APIs should document the CC0 license\n    message: \"API should include license information (CC0 1.0 Universal)\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  usda-ars-contact-info:\n    description: APIs should have contact information\n    message: \"API missing contact information\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/usda-agricultural-research-service-ars-/refs/heads/main/rules/usda-agricultural-research-service-ars--rules.yml
tags:
- Federal Government
- Agriculture
- Food Safety
- Nutrition
- Open Data
- Research
- Spectral
- Linting
- API Governance
---
