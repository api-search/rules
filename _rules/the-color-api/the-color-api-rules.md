---
api_specs:
- filename: the-color-api-openapi.yml
  format: yaml
  label: The Color API
  slug: the-color-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/the-color-api/refs/heads/main/openapi/the-color-api-openapi.yml
categories:
- colorapi
description: Spectral linting rules defining API design standards and conventions for The Color API.
layout: rules
name: The Color API API Rules
provider_name: The Color API
provider_slug: the-color-api
rule_count: 10
rules:
- description: All Color API operations must be tagged (Colors or Schemes).
  given: $.paths[*][get]
  name: colorapi-operations-must-have-tags
  severity: warn
- description: All operations must define an operationId.
  given: $.paths[*][get]
  name: colorapi-operations-must-have-operationid
  severity: error
- description: All operations must have a summary in Title Case.
  given: $.paths[*][get]
  name: colorapi-operations-must-have-summary
  severity: warn
- description: Color input parameters (hex, rgb, hsl, cmyk) should include examples.
  given: $.paths[*][get].parameters[?(@.name == 'hex' || @.name == 'rgb' || @.name == 'hsl' || @.name == 'cmyk')]
  name: colorapi-color-input-params-must-have-examples
  severity: warn
- description: The format parameter must constrain values to json, html, or svg.
  given: $.paths[*][get].parameters[?(@.name == 'format')].schema
  name: colorapi-format-param-must-use-enum
  severity: error
- description: The mode parameter must constrain values to the supported scheme modes.
  given: $.paths[*][get].parameters[?(@.name == 'mode')].schema
  name: colorapi-scheme-mode-must-use-enum
  severity: error
- description: All operations must define a 200 success response.
  given: $.paths[*][get].responses
  name: colorapi-responses-must-include-200
  severity: error
- description: All operations must define a 400 error response for invalid color input.
  given: $.paths[*][get].responses
  name: colorapi-responses-must-include-400
  severity: warn
- description: All query parameters must have descriptions.
  given: $.paths[*][get].parameters[*]
  name: colorapi-parameters-must-have-descriptions
  severity: warn
- description: All 200 responses must reference a schema.
  given: $.paths[*][get].responses.200.content.application/json
  name: colorapi-responses-must-define-content-schema
  severity: warn
rules_file: rules/the-color-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-color-api/refs/heads/main/rules/the-color-api-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: the-color-api-rules
source_filename: the-color-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  colorapi-operations-must-have-tags:\n    description: All Color API operations must be tagged (Colors or Schemes).\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: tags\n      function: truthy\n\n  colorapi-operations-must-have-operationid:\n    description: All operations must define an operationId.\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      field: operationId\n      function: truthy\n\n  colorapi-operations-must-have-summary:\n    description: All operations must have a summary in Title Case.\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: summary\n      function: truthy\n\n  colorapi-color-input-params-must-have-examples:\n    description: Color input parameters (hex, rgb, hsl, cmyk) should include examples.\n    severity: warn\n    given: \"$.paths[*][get].parameters[?(@.name == 'hex' || @.name == 'rgb' || @.name == 'hsl' || @.name == 'cmyk')]\"\n    then:\n\
  \      field: example\n      function: truthy\n\n  colorapi-format-param-must-use-enum:\n    description: The format parameter must constrain values to json, html, or svg.\n    severity: error\n    given: \"$.paths[*][get].parameters[?(@.name == 'format')].schema\"\n    then:\n      field: enum\n      function: truthy\n\n  colorapi-scheme-mode-must-use-enum:\n    description: The mode parameter must constrain values to the supported scheme modes.\n    severity: error\n    given: \"$.paths[*][get].parameters[?(@.name == 'mode')].schema\"\n    then:\n      field: enum\n      function: truthy\n\n  colorapi-responses-must-include-200:\n    description: All operations must define a 200 success response.\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  colorapi-responses-must-include-400:\n    description: All operations must define a 400 error response for invalid color input.\n    severity: warn\n    given: \"$.paths[*][get].responses\"\
  \n    then:\n      field: \"400\"\n      function: truthy\n\n  colorapi-parameters-must-have-descriptions:\n    description: All query parameters must have descriptions.\n    severity: warn\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  colorapi-responses-must-define-content-schema:\n    description: All 200 responses must reference a schema.\n    severity: warn\n    given: \"$.paths[*][get].responses.200.content.application/json\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-color-api/refs/heads/main/rules/the-color-api-rules.yml
tags:
- Colors
- Design
- Utilities
- Spectral
- Linting
- API Governance
---
