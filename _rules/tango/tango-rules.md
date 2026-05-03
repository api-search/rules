---
api_specs:
- filename: tango-raas-api-openapi.yml
  format: yaml
  label: Tango RaaS API
  slug: raas-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tango/refs/heads/main/openapi/tango-raas-api-openapi.yml
categories:
- tango
description: Spectral linting rules defining API design standards and conventions for Tango.
layout: rules
name: Tango API Rules
provider_name: Tango
provider_slug: tango
rule_count: 10
rules:
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: tango-operation-ids-camel-case
  severity: warn
- description: All path segments must use kebab-case or be a path parameter
  given: $.paths[*]~
  name: tango-paths-kebab-case
  severity: warn
- description: 2xx responses must define a content type
  given: $.paths[*][*].responses[?(@property >= 200 && @property < 300)]
  name: tango-responses-have-content-type
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: tango-parameters-have-descriptions
  severity: warn
- description: All schema components must have descriptions
  given: $.components.schemas[*]
  name: tango-schemas-have-descriptions
  severity: warn
- description: All operations must declare security requirements
  given: $.paths[*][*]
  name: tango-auth-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: tango-operations-have-tags
  severity: warn
- description: Response schemas should use $ref to reusable components
  given: $.paths[*][*].responses[*].content[*].schema
  name: tango-response-schema-refs
  severity: hint
- description: Customer identifier path parameters must be named customerIdentifier
  given: $.paths[*][*].parameters[?(@.in === 'path' && @.name === 'customerId')]
  name: tango-customer-identifier-path-param
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: tango-delete-returns-204
  severity: warn
rules_file: rules/tango-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tango/refs/heads/main/rules/tango-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 8
slug: tango-rules
source_filename: tango-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tango-operation-ids-camel-case:\n    description: All operationIds must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tango-paths-kebab-case:\n    description: All path segments must use kebab-case or be a path parameter\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z]+\\\\})+$\"\n\n  tango-responses-have-content-type:\n    description: 2xx responses must define a content type\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property >= 200 && @property < 300)]\"\n    then:\n      field: content\n      function: truthy\n\n  tango-parameters-have-descriptions:\n    description: All parameters must have descriptions\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n\
  \      field: description\n      function: truthy\n\n  tango-schemas-have-descriptions:\n    description: All schema components must have descriptions\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tango-auth-required:\n    description: All operations must declare security requirements\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [security]\n            - {}\n\n  tango-operations-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tango-response-schema-refs:\n    description: Response schemas should use $ref to reusable components\n    severity: hint\n    given: \"$.paths[*][*].responses[*].content[*].schema\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          anyOf:\n            - required: [\"$ref\"]\n            - properties:\n                type:\n                  enum: [array, object]\n\n  tango-customer-identifier-path-param:\n    description: Customer identifier path parameters must be named customerIdentifier\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in === 'path' && @.name === 'customerId')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            name:\n              const: customerIdentifier\n\n  tango-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"204\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tango/refs/heads/main/rules/tango-rules.yml
tags:
- Catalog Management
- Digital Rewards
- Gift Cards
- Incentives
- Loyalty
- Rewards As A Service
- Spectral
- Linting
- API Governance
---
