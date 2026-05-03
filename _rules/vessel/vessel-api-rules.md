---
api_specs:
- filename: vessel-platform-openapi.yml
  format: yaml
  label: Vessel Platform API
  slug: platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vessel/refs/heads/main/openapi/vessel-platform-openapi.yml
- filename: vessel-crm-openapi.yml
  format: yaml
  label: Vessel CRM API
  slug: crm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vessel/refs/heads/main/openapi/vessel-crm-openapi.yml
categories:
- vessel
description: Spectral linting rules defining API design standards and conventions for Vessel.
layout: rules
name: Vessel API Rules
provider_name: Vessel
provider_slug: vessel
rule_count: 10
rules:
- description: Operation IDs must use camelCase as per Vessel API conventions
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: vessel-operation-ids-camel-case
  severity: warn
- description: All operations must declare apiToken security scheme
  given: $.paths[*][get,post,put,patch,delete].security
  name: vessel-require-api-token-security
  severity: warn
- description: Vessel API uses POST for most operations and returns 200
  given: $.paths[*].post
  name: vessel-post-responses-should-return-200
  severity: info
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: vessel-require-operation-description
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: vessel-require-operation-tags
  severity: warn
- description: All ID fields in schemas should be type string (Vessel normalizes all IDs to strings)
  given: $.components.schemas[*].properties.id
  name: vessel-ids-should-be-strings
  severity: warn
- description: Date fields should use date-time format (Vessel normalizes all dates to ISO 8601)
  given: $.components.schemas[*].properties[*At]
  name: vessel-dates-should-be-datetime
  severity: info
- description: Error responses must include a content schema
  given: $.paths[*][get,post,put,patch,delete].responses['4*','5*'].content['application/json']
  name: vessel-error-responses-should-have-schema
  severity: warn
- description: API info must include contact information
  given: $.info
  name: vessel-require-contact-info
  severity: info
- description: The passthrough endpoint must define a request body
  given: $.paths['/passthrough'].post
  name: vessel-passthrough-must-have-request-body
  severity: warn
rules_file: rules/vessel-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vessel/refs/heads/main/rules/vessel-api-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 3
  warn: 7
slug: vessel-api-rules
source_filename: vessel-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vessel-operation-ids-camel-case:\n    description: Operation IDs must use camelCase as per Vessel API conventions\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  vessel-require-api-token-security:\n    description: All operations must declare apiToken security scheme\n    message: \"Operation must require x-vessel-api-token authentication\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].security\"\n    then:\n      function: truthy\n\n  vessel-post-responses-should-return-200:\n    description: Vessel API uses POST for most operations and returns 200\n    message: \"POST operations should return 200 (Vessel API convention)\"\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      field: responses\n   \
  \   function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '200'\n\n  vessel-require-operation-description:\n    description: All operations must have a description\n    message: \"Operation must include a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  vessel-require-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  vessel-ids-should-be-strings:\n    description: All ID fields in schemas should be type string (Vessel normalizes all IDs to strings)\n    message: \"ID fields must be type string (Vessel normalizes all IDs)\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.id\"\
  \n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  vessel-dates-should-be-datetime:\n    description: Date fields should use date-time format (Vessel normalizes all dates to ISO 8601)\n    message: \"Date fields should use format date-time\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*At]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  vessel-error-responses-should-have-schema:\n    description: Error responses must include a content schema\n    message: \"4xx and 5xx responses must include content schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses['4*','5*'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  vessel-require-contact-info:\n    description: API info must include contact information\n    message: \"API info should\
  \ include contact information\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  vessel-passthrough-must-have-request-body:\n    description: The passthrough endpoint must define a request body\n    message: \"Passthrough endpoint must have a requestBody\"\n    severity: warn\n    given: \"$.paths['/passthrough'].post\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vessel/refs/heads/main/rules/vessel-api-rules.yml
tags:
- CRM
- Embedded Integrations
- GTM
- Integrations
- iPaaS
- Sales Engagement
- Unified API
- Spectral
- Linting
- API Governance
---
