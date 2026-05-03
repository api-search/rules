---
api_specs:
- filename: cgmix-maritime-information-exchange-openapi.yml
  format: yaml
  label: CGMIX Maritime Information Exchange API
  slug: cgmix-maritime-information-exchange
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/united-states-coast-guard/refs/heads/main/openapi/cgmix-maritime-information-exchange-openapi.yml
categories:
- cgmix
description: Spectral linting rules defining API design standards and conventions for United States Coast Guard.
layout: rules
name: United States Coast Guard API Rules
provider_name: United States Coast Guard
provider_slug: united-states-coast-guard
rule_count: 7
rules:
- description: All operations must have operationIds for client generation.
  given: $.paths[*][get,post,put,delete,patch]
  name: cgmix-operation-ids-required
  severity: error
- description: PSIX endpoints require VesselID parameter.
  given: $.paths[?(@property =~ /PSIXData/)][*].parameters[?(@.name == 'VesselID')]
  name: cgmix-vessel-id-required
  severity: error
- description: CGMIX APIs return XML responses.
  given: $.paths[*][get,post].responses[*].content
  name: cgmix-xml-response-type
  severity: warn
- description: All operations should have tags for grouping.
  given: $.paths[*][get,post,put,delete,patch]
  name: cgmix-operations-have-tags
  severity: warn
- description: All parameters should include descriptions.
  given: $.paths[*][*].parameters[*]
  name: cgmix-parameters-have-descriptions
  severity: warn
- description: API info should include contact details.
  given: $.info
  name: cgmix-info-contact
  severity: warn
- description: All operations should document at least a 200 response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: cgmix-responses-documented
  severity: error
rules_file: rules/cgmix-maritime-information-exchange-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/united-states-coast-guard/refs/heads/main/rules/cgmix-maritime-information-exchange-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: cgmix-maritime-information-exchange-rules
source_filename: cgmix-maritime-information-exchange-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  cgmix-operation-ids-required:\n    description: All operations must have operationIds for client generation.\n    message: Operation must have an operationId.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n    severity: error\n\n  cgmix-vessel-id-required:\n    description: PSIX endpoints require VesselID parameter.\n    message: >-\n      PSIX vessel operations must include VesselID as a required query\n      parameter.\n    given: \"$.paths[?(@property =~ /PSIXData/)][*].parameters[?(@.name == 'VesselID')]\"\n    then:\n      field: required\n      function: truthy\n    severity: error\n\n  cgmix-xml-response-type:\n    description: CGMIX APIs return XML responses.\n    message: CGMIX operations should document text/xml response content type.\n    given: \"$.paths[*][get,post].responses[*].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \          properties:\n            text/xml:\n              type: object\n    severity: warn\n\n  cgmix-operations-have-tags:\n    description: All operations should have tags for grouping.\n    message: Operation must include at least one tag.\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n    severity: warn\n\n  cgmix-parameters-have-descriptions:\n    description: All parameters should include descriptions.\n    message: Parameter must have a description.\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  cgmix-info-contact:\n    description: API info should include contact details.\n    message: API info block must contain a contact object.\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n    severity: warn\n\n  cgmix-responses-documented:\n    description: All operations should document at least a 200 response.\n\
  \    message: Operation must document a 200 success response.\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/united-states-coast-guard/refs/heads/main/rules/cgmix-maritime-information-exchange-rules.yml
tags:
- Federal Government
- Maritime Safety
- Vessel Documentation
- Emergency Response
- Law Enforcement
- Spectral
- Linting
- API Governance
---
