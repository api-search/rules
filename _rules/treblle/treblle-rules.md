---
api_specs:
- filename: treblle-api-openapi.yml
  format: yaml
  label: Treblle Platform API
  slug: treblle-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/treblle/refs/heads/main/openapi/treblle-api-openapi.yml
categories:
- treblle
description: Spectral linting rules defining API design standards and conventions for Treblle.
layout: rules
name: Treblle API Rules
provider_name: Treblle
provider_slug: treblle
rule_count: 7
rules:
- description: All Treblle API operations should have an operationId for consistent SDK generation and documentation.
  given: $.paths[*][get,post,put,patch,delete]
  name: treblle-operation-id-required
  severity: error
- description: Treblle API uses API key authentication via the Treblle-Api-Key header. All operations should declare security requirements.
  given: $.paths[*][*]
  name: treblle-api-key-auth
  severity: warn
- description: All Treblle API GET operations should define a 200 response.
  given: $.paths[*].get.responses
  name: treblle-response-200-defined
  severity: warn
- description: All Treblle API operations requiring authentication should document the 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: treblle-response-401-defined
  severity: warn
- description: All operations should be tagged for catalog navigation.
  given: $.paths[*][*].tags
  name: treblle-tags-required
  severity: warn
- description: All operations should have a clear description.
  given: $.paths[*][*]
  name: treblle-description-required
  severity: warn
- description: All operations should have a summary for quick identification.
  given: $.paths[*][*]
  name: treblle-summary-required
  severity: error
rules_file: rules/treblle-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/treblle/refs/heads/main/rules/treblle-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: treblle-rules
source_filename: treblle-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  treblle-operation-id-required:\n    description: >-\n      All Treblle API operations should have an operationId for consistent\n      SDK generation and documentation.\n    message: \"Operation should have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  treblle-api-key-auth:\n    description: >-\n      Treblle API uses API key authentication via the Treblle-Api-Key header.\n      All operations should declare security requirements.\n    message: \"Operation should declare security requirements\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"security\"]\n            - not:\n                required: [\"security\"]\n\n  treblle-response-200-defined:\n    description: All Treblle API GET operations should define\
  \ a 200 response.\n    message: \"GET operation should define a 200 response\"\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"200\"]\n\n  treblle-response-401-defined:\n    description: >-\n      All Treblle API operations requiring authentication should document\n      the 401 Unauthorized response.\n    message: \"Operation should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  treblle-tags-required:\n    description: All operations should be tagged for catalog navigation.\n    message: \"Operation should have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  treblle-description-required:\n\
  \    description: All operations should have a clear description.\n    message: \"Operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  treblle-summary-required:\n    description: All operations should have a summary for quick identification.\n    message: \"Operation should have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/treblle/refs/heads/main/rules/treblle-rules.yml
tags:
- Analytics
- Artificial Intelligence
- Developer Experience
- Documentation
- Governance
- Insights
- Observability
- Platform
- Security
- Testing
- Spectral
- Linting
- API Governance
---
