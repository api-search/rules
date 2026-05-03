---
api_specs:
- filename: yaml-spec
  format: yaml
  label: USDA FoodData Central API
  slug: usda-fooddata-central-api
  spec_type: OpenAPI
  url: https://api.nal.usda.gov/fdc/v1/yaml-spec?api_key=DEMO_KEY
- filename: usda-nass-quickstats-openapi.yml
  format: yaml
  label: USDA NASS Quick Stats API
  slug: usda-nass-quickstats-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-department-of-agriculture/refs/heads/main/openapi/usda-nass-quickstats-openapi.yml
- filename: usda-ers-arms-openapi.yml
  format: yaml
  label: USDA ERS ARMS Data API
  slug: usda-ers-arms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-department-of-agriculture/refs/heads/main/openapi/usda-ers-arms-openapi.yml
- filename: usda-nrcs-awdb-openapi.yml
  format: yaml
  label: USDA NRCS AWDB Water and Climate REST API
  slug: usda-nrcs-awdb-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-department-of-agriculture/refs/heads/main/openapi/usda-nrcs-awdb-openapi.yml
categories:
- usda
description: Spectral linting rules defining API design standards and conventions for United States Department of Agriculture.
layout: rules
name: United States Department of Agriculture API Rules
provider_name: United States Department of Agriculture
provider_slug: united-states-department-of-agriculture
rule_count: 7
rules:
- description: All operations must have operationIds.
  given: $.paths[*][get,post,put,delete,patch]
  name: usda-fdc-operation-ids
  severity: error
- description: FoodData Central endpoints require api_key parameter.
  given: $.paths[*][get].parameters[?(@.name == 'api_key')]
  name: usda-fdc-api-key-param
  severity: error
- description: All operations must have tags.
  given: $.paths[*][get,post,put,delete,patch]
  name: usda-fdc-operations-have-tags
  severity: warn
- description: All parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: usda-fdc-parameters-have-descriptions
  severity: warn
- description: Operations must document 200 responses.
  given: $.paths[*][get,post].responses
  name: usda-fdc-success-responses
  severity: error
- description: FoodData Central operations should return JSON.
  given: $.paths[*][get,post].responses.200.content
  name: usda-fdc-json-responses
  severity: warn
- description: All schema components should have descriptions.
  given: $.components.schemas[*]
  name: usda-fdc-schemas-have-descriptions
  severity: warn
rules_file: rules/usda-fooddata-central-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-department-of-agriculture/refs/heads/main/rules/usda-fooddata-central-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: usda-fooddata-central-rules
source_filename: usda-fooddata-central-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  usda-fdc-operation-ids:\n    description: All operations must have operationIds.\n    message: Operation must have an operationId.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n    severity: error\n\n  usda-fdc-api-key-param:\n    description: FoodData Central endpoints require api_key parameter.\n    message: FDC operations must include api_key query parameter.\n    given: \"$.paths[*][get].parameters[?(@.name == 'api_key')]\"\n    then:\n      field: required\n      function: truthy\n    severity: error\n\n  usda-fdc-operations-have-tags:\n    description: All operations must have tags.\n    message: Operation must include at least one tag.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  usda-fdc-parameters-have-descriptions:\n    description: All parameters should have descriptions.\n    message: Parameter must\
  \ have a description.\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  usda-fdc-success-responses:\n    description: Operations must document 200 responses.\n    message: Operation must document a 200 success response.\n    given: \"$.paths[*][get,post].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n\n  usda-fdc-json-responses:\n    description: FoodData Central operations should return JSON.\n    message: >-\n      FDC API operations should document application/json response content type.\n    given: \"$.paths[*][get,post].responses.200.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            application/json:\n              type: object\n    severity: warn\n\n  usda-fdc-schemas-have-descriptions:\n    description: All schema components should have descriptions.\n    message:\
  \ Schema component must have a description.\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-department-of-agriculture/refs/heads/main/rules/usda-fooddata-central-rules.yml
tags:
- Federal Government
- Agriculture
- Food Safety
- Nutrition
- Rural Development
- Climate
- Spectral
- Linting
- API Governance
---
