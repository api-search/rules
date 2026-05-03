---
api_specs:
- filename: techrepublic-wordpress-rest-api-openapi.yml
  format: yaml
  label: TechRepublic WordPress REST API
  slug: wordpress-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/techrepublic/refs/heads/main/openapi/techrepublic-wordpress-rest-api-openapi.yml
categories:
- techrepublic
description: Spectral linting rules defining API design standards and conventions for TechRepublic.
layout: rules
name: TechRepublic API Rules
provider_name: TechRepublic
provider_slug: techrepublic
rule_count: 12
rules:
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: techrepublic-operation-ids-camel-case
  severity: warn
- description: Collection endpoints must support page and per_page query parameters.
  given: $.paths[*].get
  name: techrepublic-pagination-parameters
  severity: warn
- description: Collection endpoints must return an array schema.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: techrepublic-response-array-for-collections
  severity: error
- description: Resource ID path parameters must use {id} naming.
  given: $.paths[*][*].parameters[*]
  name: techrepublic-path-ids-in-path
  severity: warn
- description: All responses must have a description.
  given: $.paths[*][*].responses[*]
  name: techrepublic-responses-have-descriptions
  severity: error
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: techrepublic-operations-have-tags
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: techrepublic-operations-have-summaries
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: techrepublic-title-case-summaries
  severity: warn
- description: API must define reusable schemas in components.
  given: $.components
  name: techrepublic-components-schemas-defined
  severity: warn
- description: All paths must have at least one operation defined.
  given: $.paths[*]
  name: techrepublic-no-empty-paths
  severity: error
- description: API info must include a contact.
  given: $.info
  name: techrepublic-info-contact
  severity: warn
- description: API must define at least one server.
  given: $
  name: techrepublic-servers-defined
  severity: error
rules_file: rules/techrepublic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/techrepublic/refs/heads/main/rules/techrepublic-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 7
slug: techrepublic-rules
source_filename: techrepublic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # TechRepublic WordPress REST API conventions\n\n  techrepublic-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., listPosts, getPost).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  techrepublic-pagination-parameters:\n    description: Collection endpoints must support page and per_page query parameters.\n    message: \"Collection GET endpoints should include 'page' and 'per_page' query parameters.\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            parameters:\n              type: array\n\n  techrepublic-response-array-for-collections:\n    description: Collection endpoints\
  \ must return an array schema.\n    message: \"Collection endpoints (list*) must return an array in their 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  techrepublic-path-ids-in-path:\n    description: Resource ID path parameters must use {id} naming.\n    message: \"Path parameter for resource identifier should be named 'id'.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  techrepublic-responses-have-descriptions:\n    description: All responses must have a description.\n    message: \"Response must include a description.\"\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  techrepublic-operations-have-tags:\n    description:\
  \ All operations must be tagged.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  techrepublic-operations-have-summaries:\n    description: All operations must have a summary.\n    message: \"Operation must include a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  techrepublic-title-case-summaries:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  techrepublic-components-schemas-defined:\n    description: API must define reusable schemas in components.\n    message: \"API should define schemas in components/schemas.\"\n    severity: warn\n    given: \"$.components\"\
  \n    then:\n      field: schemas\n      function: truthy\n\n  techrepublic-no-empty-paths:\n    description: All paths must have at least one operation defined.\n    message: \"Path '{{path}}' has no operations defined.\"\n    severity: error\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  techrepublic-info-contact:\n    description: API info must include a contact.\n    message: \"API info should include a contact URL or email.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  techrepublic-servers-defined:\n    description: API must define at least one server.\n    message: \"API must include a servers array with at least one entry.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/techrepublic/refs/heads/main/rules/techrepublic-rules.yml
tags:
- Enterprise IT
- Media
- Technology News
- Content
- Publishing
- Spectral
- Linting
- API Governance
---
