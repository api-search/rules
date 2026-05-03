---
api_specs:
- filename: thespacedevs-ll2-api-openapi.yml
  format: yaml
  label: TheSpaceDevs Launch Library 2 API
  slug: thespacedevs-ll2-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thespacedevs-ll2-api/refs/heads/main/openapi/thespacedevs-ll2-api-openapi.yml
categories:
- thespacedevs
description: Spectral linting rules defining API design standards and conventions for TheSpaceDevs LL2 API.
layout: rules
name: TheSpaceDevs LL2 API API Rules
provider_name: TheSpaceDevs LL2 API
provider_slug: thespacedevs-ll2-api
rule_count: 9
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thespacedevs-operation-summary-title-case
  severity: warn
- description: LL2 API uses snake_case operationIds in format resource_action.
  given: $.paths[*][*].operationId
  name: thespacedevs-operation-ids-snake-case
  severity: info
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: thespacedevs-tags-required
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: thespacedevs-description-required
  severity: info
- description: All GET operations must define a 200 response.
  given: $.paths[*][get].responses
  name: thespacedevs-200-response-defined
  severity: error
- description: List operations should support a limit query parameter.
  given: $.paths[*~][?(@.get)]
  name: thespacedevs-list-has-limit-param
  severity: info
- description: All paths should include the API version prefix /2.3.0/.
  given: $.paths[*]~
  name: thespacedevs-path-version-prefix
  severity: warn
- description: LL2 API paths use trailing slashes.
  given: $.paths[*]~
  name: thespacedevs-path-trailing-slash
  severity: info
- description: At least one server URL must be defined.
  given: $
  name: thespacedevs-servers-defined
  severity: error
rules_file: rules/thespacedevs-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thespacedevs-ll2-api/refs/heads/main/rules/thespacedevs-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 3
slug: thespacedevs-rules
source_filename: thespacedevs-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  thespacedevs-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  thespacedevs-operation-ids-snake-case:\n    description: LL2 API uses snake_case operationIds in format resource_action.\n    message: \"OperationId '{{value}}' should use snake_case (resource_action pattern).\"\n    severity: info\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  thespacedevs-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation at '{{path}}' must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n\
  \      function: truthy\n\n  thespacedevs-description-required:\n    description: All operations should have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  thespacedevs-200-response-defined:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  thespacedevs-list-has-limit-param:\n    description: List operations should support a limit query parameter.\n    message: \"List operation at '{{path}}' should support 'limit' parameter.\"\n    severity: info\n    given: \"$.paths[*~][?(@.get)]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  thespacedevs-path-version-prefix:\n\
  \    description: All paths should include the API version prefix /2.3.0/.\n    message: \"Path '{{path}}' should start with the API version prefix /2.3.0/.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/2\\\\.3\\\\.0\\\\/\"\n\n  thespacedevs-path-trailing-slash:\n    description: LL2 API paths use trailing slashes.\n    message: \"Path '{{path}}' should end with a trailing slash per LL2 API convention.\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\/$\"\n\n  thespacedevs-servers-defined:\n    description: At least one server URL must be defined.\n    message: \"No server URLs defined.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thespacedevs-ll2-api/refs/heads/main/rules/thespacedevs-rules.yml
tags:
- Space
- Satellites
- Launches
- Rockets
- Astronauts
- Spectral
- Linting
- API Governance
---
