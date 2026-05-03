---
api_specs:
- filename: vite-javascript-api-openapi.yml
  format: yaml
  label: Vite JavaScript API
  slug: javascript-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vite/refs/heads/main/openapi/vite-javascript-api-openapi.yml
- filename: vite-plugin-api-openapi.yml
  format: yaml
  label: Vite Plugin API
  slug: plugin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vite/refs/heads/main/openapi/vite-plugin-api-openapi.yml
categories:
- vite
description: Spectral linting rules defining API design standards and conventions for Vite.
layout: rules
name: Vite API Rules
provider_name: Vite
provider_slug: vite
rule_count: 9
rules:
- description: Operation IDs must use camelCase to match Vite's JavaScript API naming conventions.
  given: $.paths[*][*].operationId
  name: vite-operation-ids-camel-case
  severity: warn
- description: All operations must be tagged for proper documentation grouping.
  given: $.paths[*][*]
  name: vite-paths-must-have-tags
  severity: warn
- description: All operations must have a human-readable summary.
  given: $.paths[*][*]
  name: vite-require-operation-summaries
  severity: error
- description: All operations, schemas, and parameters must have descriptions for developer clarity.
  given:
  - $.paths[*][*]
  - $.components.schemas[*]
  - $.paths[*][*].parameters[*]
  name: vite-require-descriptions
  severity: warn
- description: All paths must start with a forward slash.
  given: $.paths
  name: vite-server-paths-start-with-slash
  severity: error
- description: All schema properties must define an explicit type for TypeScript interoperability.
  given: $.components.schemas[*].properties[*]
  name: vite-schema-properties-have-types
  severity: warn
- description: Vite API specs must use OpenAPI 3.1.0 to leverage full JSON Schema support.
  given: $
  name: vite-use-openapi-31
  severity: error
- description: API info must include contact information pointing to the Vite team.
  given: $.info
  name: vite-info-contact-required
  severity: warn
- description: GET operations must always define a 200 success response.
  given: $.paths[*].get
  name: vite-responses-have-200
  severity: error
rules_file: rules/vite-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vite/refs/heads/main/rules/vite-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: vite-rules
source_filename: vite-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Vite API conventions\n  vite-operation-ids-camel-case:\n    description: Operation IDs must use camelCase to match Vite's JavaScript API naming conventions.\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vite-paths-must-have-tags:\n    description: All operations must be tagged for proper documentation grouping.\n    message: \"Operation {{path}} must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  vite-require-operation-summaries:\n    description: All operations must have a human-readable summary.\n    message: \"Operation {{path}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  vite-require-descriptions:\n\
  \    description: All operations, schemas, and parameters must have descriptions for developer clarity.\n    message: \"{{path}} must have a description\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.components.schemas[*]\"\n      - \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  vite-server-paths-start-with-slash:\n    description: All paths must start with a forward slash.\n    message: \"Path {{path}} must start with /\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/\"\n\n  vite-schema-properties-have-types:\n    description: All schema properties must define an explicit type for TypeScript interoperability.\n    message: \"Schema property {{path}} must have a type\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n\n  vite-use-openapi-31:\n    description:\
  \ Vite API specs must use OpenAPI 3.1.0 to leverage full JSON Schema support.\n    message: \"OpenAPI version must be 3.1.0\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  vite-info-contact-required:\n    description: API info must include contact information pointing to the Vite team.\n    message: \"Info object must include a contact field\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  vite-responses-have-200:\n    description: GET operations must always define a 200 success response.\n    message: \"GET operation {{path}} must define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vite/refs/heads/main/rules/vite-rules.yml
tags:
- Build Tools
- Bundler
- Development Server
- ESM
- Frontend
- Hot Module Replacement
- JavaScript
- Plugin API
- TypeScript
- Vite
- Spectral
- Linting
- API Governance
---
