---
api_specs:
- filename: rsc-chemspider-compounds-openapi.yml
  format: yaml
  label: ChemSpider Compounds API
  slug: chemspider-compounds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rsc/refs/heads/main/openapi/rsc-chemspider-compounds-openapi.yml
- filename: rsc-chemspider-compounds-openapi.yml
  format: yaml
  label: ChemSpider Tools API
  slug: chemspider-tools
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rsc/refs/heads/main/openapi/rsc-chemspider-compounds-openapi.yml
categories:
- rsc
description: Spectral linting rules defining API design standards and conventions for RSC.
layout: rules
name: RSC API Rules
provider_name: RSC
provider_slug: rsc
rule_count: 8
rules:
- description: All operationIds must use camelCase naming convention.
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: rsc-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: rsc-tags-title-case
  severity: warn
- description: All operations must use apiKeyAuth security unless explicitly public.
  given: $.paths.*[get,post,put,patch,delete]
  name: rsc-api-key-auth
  severity: warn
- description: POST request bodies must use application/json content type.
  given: $.paths.*.post.requestBody.content
  name: rsc-request-body-json
  severity: warn
- description: Filter endpoints should return a queryId for async polling.
  given: $.paths['/filter/*'].post.responses.200.content.application/json.schema
  name: rsc-filter-endpoints-return-query-id
  severity: info
- description: All path segments must use kebab-case.
  given: $.paths
  name: rsc-paths-kebab-case
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: rsc-response-200-defined
  severity: error
- description: Secured operations should define a 401 response.
  given: $.paths.*[get,post].responses
  name: rsc-401-defined-for-secured
  severity: warn
rules_file: rules/rsc-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rsc/refs/heads/main/rules/rsc-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 6
slug: rsc-spectral-rules
source_filename: rsc-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rsc-operation-ids-camel-case:\n    description: All operationIds must use camelCase naming convention.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rsc-tags-title-case:\n    description: All tags must use Title Case.\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  rsc-api-key-auth:\n    description: All operations must use apiKeyAuth security unless explicitly public.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  rsc-request-body-json:\n    description: POST request bodies must use application/json\
  \ content type.\n    severity: warn\n    given: \"$.paths.*.post.requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            application/json:\n              type: object\n\n  rsc-filter-endpoints-return-query-id:\n    description: Filter endpoints should return a queryId for async polling.\n    severity: info\n    given: \"$.paths['/filter/*'].post.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            queryId:\n              type: string\n\n  rsc-paths-kebab-case:\n    description: All path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  rsc-response-200-defined:\n    description: All operations must define a 200 response.\n    severity: error\n    given: \"\
  $.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - \"200\"\n\n  rsc-401-defined-for-secured:\n    description: Secured operations should define a 401 response.\n    severity: warn\n    given: \"$.paths.*[get,post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            \"401\":\n              type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rsc/refs/heads/main/rules/rsc-spectral-rules.yml
tags:
- Chemistry
- Cheminformatics
- Chemical Data
- Science
- Spectral
- Linting
- API Governance
---
