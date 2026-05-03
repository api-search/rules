---
api_specs:
- filename: teledyne-flir-camera-rest-openapi.yml
  format: yaml
  label: Teledyne FLIR Camera REST API
  slug: flir-camera-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/teledyne-technologies/refs/heads/main/openapi/teledyne-flir-camera-rest-openapi.yml
categories:
- teledyne
description: Spectral linting rules defining API design standards and conventions for Teledyne Technologies.
layout: rules
name: Teledyne Technologies API Rules
provider_name: Teledyne Technologies
provider_slug: teledyne-technologies
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: teledyne-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: teledyne-operations-have-summaries
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: teledyne-title-case-summaries
  severity: warn
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: teledyne-operations-have-tags
  severity: warn
- description: All responses must have descriptions.
  given: $.paths[*][*].responses[*]
  name: teledyne-responses-have-descriptions
  severity: error
- description: API must define at least one server.
  given: $
  name: teledyne-servers-defined
  severity: error
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in === 'path')]
  name: teledyne-path-parameters-described
  severity: warn
- description: JSON-returning endpoints must define response schemas.
  given: $.paths[*][*].responses[200].content.application/json
  name: teledyne-json-responses-defined
  severity: warn
- description: Temperature unit parameters should use standard C/F/K enum.
  given: $.paths[*][*].parameters[?(@.name === 'tempUnit')]
  name: teledyne-temp-unit-enum
  severity: hint
- description: API must define reusable schemas.
  given: $.components
  name: teledyne-components-schemas
  severity: warn
rules_file: rules/teledyne-technologies-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/teledyne-technologies/refs/heads/main/rules/teledyne-technologies-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: teledyne-technologies-rules
source_filename: teledyne-technologies-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  teledyne-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  teledyne-operations-have-summaries:\n    description: All operations must have a summary.\n    message: \"Operation must include a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  teledyne-title-case-summaries:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  teledyne-operations-have-tags:\n    description:\
  \ All operations must be tagged.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  teledyne-responses-have-descriptions:\n    description: All responses must have descriptions.\n    message: \"Response must include a description.\"\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  teledyne-servers-defined:\n    description: API must define at least one server.\n    message: \"API must include a servers array with at least one entry.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  teledyne-path-parameters-described:\n    description: All path parameters must have descriptions.\n    message: \"Path parameter must include a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in === 'path')]\"\n    then:\n      field:\
  \ description\n      function: truthy\n\n  teledyne-json-responses-defined:\n    description: JSON-returning endpoints must define response schemas.\n    message: \"JSON response should define a schema.\"\n    severity: warn\n    given: \"$.paths[*][*].responses[200].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  teledyne-temp-unit-enum:\n    description: Temperature unit parameters should use standard C/F/K enum.\n    message: \"Temperature unit should be one of: C, F, K.\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.name === 'tempUnit')]\"\n    then:\n      field: schema\n      function: truthy\n\n  teledyne-components-schemas:\n    description: API must define reusable schemas.\n    message: \"API should define schemas in components/schemas.\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/teledyne-technologies/refs/heads/main/rules/teledyne-technologies-rules.yml
tags:
- Aerospace
- Defense
- Digital Imaging
- Instrumentation
- Thermal Imaging
- Test and Measurement
- Fortune 500
- Spectral
- Linting
- API Governance
---
