---
api_specs:
- filename: openfema-fire-data-openapi.yml
  format: yaml
  label: OpenFEMA Fire Data API
  slug: openfema-fire-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-fire-administration/refs/heads/main/openapi/openfema-fire-data-openapi.yml
categories:
- openfema
description: Spectral linting rules defining API design standards and conventions for United States Fire Administration.
layout: rules
name: United States Fire Administration API Rules
provider_name: United States Fire Administration
provider_slug: united-states-fire-administration
rule_count: 7
rules:
- description: All operations must have operationIds.
  given: $.paths[*][get,post,put,delete,patch]
  name: openfema-operation-ids-required
  severity: error
- description: All operations should be tagged for grouping.
  given: $.paths[*][get,post,put,delete,patch]
  name: openfema-operations-have-tags
  severity: warn
- description: All query parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: openfema-parameters-have-descriptions
  severity: warn
- description: All operations must document 200 success response.
  given: $.paths[*][get,post].responses
  name: openfema-success-responses
  severity: error
- description: OpenFEMA operations should support JSON responses.
  given: $.paths[*][get].responses.200.content
  name: openfema-json-responses
  severity: warn
- description: Schema components should have descriptions.
  given: $.components.schemas[*]
  name: openfema-schemas-have-descriptions
  severity: warn
- description: API info should include contact information.
  given: $.info
  name: openfema-info-contact
  severity: warn
rules_file: rules/openfema-fire-data-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-fire-administration/refs/heads/main/rules/openfema-fire-data-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: openfema-fire-data-rules
source_filename: openfema-fire-data-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  openfema-operation-ids-required:\n    description: All operations must have operationIds.\n    message: Operation must have an operationId.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n    severity: error\n\n  openfema-operations-have-tags:\n    description: All operations should be tagged for grouping.\n    message: Operation must include at least one tag.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  openfema-parameters-have-descriptions:\n    description: All query parameters should have descriptions.\n    message: Parameter must have a description.\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  openfema-success-responses:\n    description: All operations must document 200 success response.\n    message: Operation must document\
  \ a 200 success response.\n    given: \"$.paths[*][get,post].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n\n  openfema-json-responses:\n    description: OpenFEMA operations should support JSON responses.\n    message: >-\n      OpenFEMA API operations should document application/json response content type.\n    given: \"$.paths[*][get].responses.200.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            application/json:\n              type: object\n    severity: warn\n\n  openfema-schemas-have-descriptions:\n    description: Schema components should have descriptions.\n    message: Schema component must include a description.\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  openfema-info-contact:\n    description: API info should include contact information.\n    message: API\
  \ info block must contain a contact object.\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n    severity: warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-fire-administration/refs/heads/main/rules/openfema-fire-data-rules.yml
tags:
- Federal Government
- Fire Safety
- Emergency Management
- Public Safety
- FEMA
- Spectral
- Linting
- API Governance
---
