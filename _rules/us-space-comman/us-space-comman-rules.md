---
api_specs:
- filename: us-space-command-space-track-openapi.yml
  format: yaml
  label: Space-Track.org REST API
  slug: space-track-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-space-comman/refs/heads/main/openapi/us-space-command-space-track-openapi.yml
categories:
- space
description: Spectral linting rules defining API design standards and conventions for US Space Command.
layout: rules
name: US Space Command API Rules
provider_name: US Space Command
provider_slug: us-space-comman
rule_count: 6
rules:
- description: Space-Track paths should follow /basicspacedata/query/class/{class}/ pattern
  given: $.paths[*]~
  name: space-track-path-class-prefix
  severity: info
- description: All operations must have a summary
  given: $.paths[*][*]
  name: space-track-operation-summary
  severity: error
- description: Operations must have at least one tag
  given: $.paths[*][*]
  name: space-track-operation-tags
  severity: warn
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: space-track-get-200-response
  severity: error
- description: Space-Track endpoints should include a format path parameter
  given: $.paths[*]~
  name: space-track-format-path-param
  severity: info
- description: Authenticated endpoints should document 401 response
  given: $.paths[*].get
  name: space-track-401-response
  severity: warn
rules_file: rules/us-space-comman-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-space-comman/refs/heads/main/rules/us-space-comman-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 2
slug: us-space-comman-rules
source_filename: us-space-comman-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  space-track-path-class-prefix:\n    description: Space-Track paths should follow /basicspacedata/query/class/{class}/ pattern\n    message: \"Space-Track paths should use /basicspacedata/query/class/ prefix\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(basicspacedata|ajaxauth|expandedspacedata)/\"\n\n  space-track-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation missing summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  space-track-operation-tags:\n    description: Operations must have at least one tag\n    message: \"Operation has no tags\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  space-track-get-200-response:\n    description: GET operations must define a 200 response\n\
  \    message: \"GET operation missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  space-track-format-path-param:\n    description: Space-Track endpoints should include a format path parameter\n    message: \"Endpoint path should include format parameter\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/format/\"\n\n  space-track-401-response:\n    description: Authenticated endpoints should document 401 response\n    message: \"Authenticated endpoint missing 401 response\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.401\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-space-comman/refs/heads/main/rules/us-space-comman-rules.yml
tags:
- Federal Government
- Space
- Space Situational Awareness
- Satellite Tracking
- Open Data
- Spectral
- Linting
- API Governance
---
