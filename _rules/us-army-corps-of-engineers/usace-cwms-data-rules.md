---
api_specs:
- filename: usace-cwms-data-openapi.yml
  format: yaml
  label: USACE CWMS Data API
  slug: usace-cwms-data
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-army-corps-of-engineers/refs/heads/main/openapi/usace-cwms-data-openapi.yml
categories:
- usace
description: Spectral linting rules defining API design standards and conventions for US Army Corps of Engineers.
layout: rules
name: US Army Corps of Engineers API Rules
provider_name: US Army Corps of Engineers
provider_slug: us-army-corps-of-engineers
rule_count: 8
rules:
- description: All USACE CWMS Data API operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: usace-operations-have-tags
  severity: warn
- description: Operation IDs should use camelCase as per USACE API conventions
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: usace-operation-ids-kebab-case
  severity: warn
- description: All query parameters should have descriptions for CWMS API usability
  given: $.paths[*][*].parameters[?(@.in == 'query')]
  name: usace-parameters-have-descriptions
  severity: warn
- description: CWMS Data API uses page-size parameter for pagination
  given: $.paths[*][get].parameters[*]
  name: usace-pagination-page-size
  severity: info
- description: All GET operations must define a 200 response
  given: $.paths[*][get]
  name: usace-response-200-defined
  severity: error
- description: Error responses should reference the Error schema
  given: $.paths[*][*].responses[?(@property >= '400')]
  name: usace-error-schema-defined
  severity: warn
- description: API paths should not have trailing slashes
  given: $.paths
  name: usace-no-trailing-slash
  severity: warn
- description: USACE API servers must use HTTPS
  given: $.servers[*].url
  name: usace-server-url-https
  severity: error
rules_file: rules/usace-cwms-data-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-army-corps-of-engineers/refs/heads/main/rules/usace-cwms-data-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: usace-cwms-data-rules
source_filename: usace-cwms-data-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  usace-operations-have-tags:\n    description: All USACE CWMS Data API operations must have at least one tag for grouping\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  usace-operation-ids-kebab-case:\n    description: Operation IDs should use camelCase as per USACE API conventions\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  usace-parameters-have-descriptions:\n    description: All query parameters should have descriptions for CWMS API usability\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'query')]\"\n    then:\n      field: description\n      function: truthy\n\n  usace-pagination-page-size:\n    description: CWMS Data API uses page-size parameter for pagination\n    severity: info\n    given:\
  \ \"$.paths[*][get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          if:\n            properties:\n              name:\n                const: page-size\n          then:\n            properties:\n              schema:\n                properties:\n                  type:\n                    const: integer\n\n  usace-response-200-defined:\n    description: All GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  usace-error-schema-defined:\n    description: Error responses should reference the Error schema\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= '400')]\"\n    then:\n      field: content\n      function: truthy\n\n  usace-no-trailing-slash:\n    description: API paths should not have trailing slashes\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        notMatch: \".*/$\"\n\n  usace-server-url-https:\n    description: USACE API servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-army-corps-of-engineers/refs/heads/main/rules/usace-cwms-data-rules.yml
tags:
- Water Resources
- Federal Government
- Military Engineering
- Infrastructure
- Open Data
- Geospatial Data
- Spectral
- Linting
- API Governance
---
