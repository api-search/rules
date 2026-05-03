---
api_specs:
- filename: salesloft-openapi.yml
  format: yaml
  label: Salesloft API
  slug: salesloft-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesloft/refs/heads/main/openapi/salesloft-openapi.yml
categories:
- salesloft
description: Spectral linting rules defining API design standards and conventions for Salesloft.
layout: rules
name: Salesloft API Rules
provider_name: Salesloft
provider_slug: salesloft
rule_count: 12
rules:
- description: All operation summaries must begin with "Salesloft" provider prefix
  given: $.paths[*][*].summary
  name: salesloft-summary-provider-prefix
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesloft-summary-title-case
  severity: hint
- description: Operations should define security requirements
  given: $.paths[*][get,post,put,delete]
  name: salesloft-security-defined
  severity: hint
- description: Tags must use Title Case
  given: $.tags[*].name
  name: salesloft-tags-title-case
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths
  name: salesloft-paths-kebab-case
  severity: hint
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: salesloft-operation-tags-required
  severity: warn
- description: Operations must define response codes
  given: $.paths[*][get,post,put,patch,delete]
  name: salesloft-responses-required
  severity: error
- description: GET operations should define a 200 response
  given: $.paths[*].get
  name: salesloft-get-200-response
  severity: warn
- description: POST operations should define a 200 or 201 response
  given: $.paths[*].post
  name: salesloft-post-success-response
  severity: hint
- description: API must have an info title
  given: $.info
  name: salesloft-info-title
  severity: error
- description: API must have an info description
  given: $.info
  name: salesloft-info-description
  severity: warn
- description: API must define servers
  given: $
  name: salesloft-servers-defined
  severity: error
rules_file: rules/salesloft-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesloft/refs/heads/main/rules/salesloft-rules.yml
severity_counts:
  error: 3
  hint: 4
  info: 0
  warn: 5
slug: salesloft-rules
source_filename: salesloft-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Salesloft requires all operation summaries to begin with \"Salesloft\" provider prefix\n  salesloft-summary-provider-prefix:\n    description: All operation summaries must begin with \"Salesloft\" provider prefix\n    message: \"Summary '{{value}}' must start with 'Salesloft'\"\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Salesloft \"\n    severity: warn\n\n  # All summaries must use Title Case\n  salesloft-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z0-9]*|\\\\s(a|an|the|and|or|for|of|in|to|by|at))*$\"\n    severity: hint\n\n  # Salesloft uses OAuth2 / Bearer token auth - operations must reference security\n  salesloft-security-defined:\n\
  \    description: Operations should define security requirements\n    message: \"Operation '{{path}}' should have security defined\"\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      - field: security\n        function: truthy\n    severity: hint\n\n  # All tags must use Title Case\n  salesloft-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' should use Title Case\"\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n    severity: warn\n\n  # Paths should use kebab-case\n  salesloft-paths-kebab-case:\n    description: Path segments should use kebab-case\n    message: \"Path '{{path}}' should use kebab-case\"\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9_{}\\\\-]+)+$\"\n    severity: hint\n\n  # Operations must have at least one tag\n  salesloft-operation-tags-required:\n    description: Operations\
  \ must have at least one tag\n    message: \"Operation '{{path}}' must have at least one tag\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - field: tags\n        function: truthy\n    severity: warn\n\n  # Response codes must be defined\n  salesloft-responses-required:\n    description: Operations must define response codes\n    message: \"Operation '{{path}}' must define at least one response\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - field: responses\n        function: truthy\n    severity: error\n\n  # GET operations should have a 200 response\n  salesloft-get-200-response:\n    description: GET operations should define a 200 response\n    message: \"GET operation at '{{path}}' should have a 200 response\"\n    given: \"$.paths[*].get\"\n    then:\n      - field: responses.200\n        function: truthy\n    severity: warn\n\n  # POST operations should have a 200 or 201 response\n  salesloft-post-success-response:\n    description:\
  \ POST operations should define a 200 or 201 response\n    message: \"POST operation at '{{path}}' should have a 200 or 201 response\"\n    given: \"$.paths[*].post\"\n    then:\n      - field: responses\n        function: schema\n        functionOptions:\n          schema:\n            anyOf:\n              - required: [\"200\"]\n              - required: [\"201\"]\n    severity: hint\n\n  # Info title must be present\n  salesloft-info-title:\n    description: API must have an info title\n    message: \"API info.title is required\"\n    given: \"$.info\"\n    then:\n      - field: title\n        function: truthy\n    severity: error\n\n  # Info description must be present\n  salesloft-info-description:\n    description: API must have an info description\n    message: \"API info.description is required\"\n    given: \"$.info\"\n    then:\n      - field: description\n        function: truthy\n    severity: warn\n\n  # Servers must be defined\n  salesloft-servers-defined:\n    description:\
  \ API must define servers\n    message: \"API must have at least one server defined\"\n    given: \"$\"\n    then:\n      - field: servers\n        function: truthy\n    severity: error\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesloft/refs/heads/main/rules/salesloft-rules.yml
tags:
- Sales
- CRM
- Revenue
- Automation
- AI
- Spectral
- Linting
- API Governance
---
