---
api_specs:
- filename: taylor-morrison-home-search-openapi.yml
  format: yaml
  label: Taylor Morrison Home Search API
  slug: taylor-morrison-home-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/taylor-morrison-home/refs/heads/main/openapi/taylor-morrison-home-search-openapi.yml
categories:
- taylor
description: Spectral linting rules defining API design standards and conventions for taylor-morrison-home.
layout: rules
name: taylor-morrison-home API Rules
provider_name: taylor-morrison-home
provider_slug: taylor-morrison-home
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: taylor-morrison-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: taylor-morrison-path-kebab-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: taylor-morrison-operation-summary-exists
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: taylor-morrison-operation-description-exists
  severity: warn
- description: All operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: taylor-morrison-responses-success
  severity: error
- description: Tags must use Title Case
  given: $.tags[*].name
  name: taylor-morrison-tags-title-case
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: taylor-morrison-parameters-description
  severity: warn
- description: API must include contact info
  given: $.info
  name: taylor-morrison-info-contact
  severity: warn
rules_file: rules/taylor-morrison-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/taylor-morrison-home/refs/heads/main/rules/taylor-morrison-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: taylor-morrison-spectral-rules
source_filename: taylor-morrison-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  taylor-morrison-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  taylor-morrison-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment must use kebab-case: {{path}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*$\"\n\n  taylor-morrison-operation-summary-exists:\n    description: All operations must have a summary\n    message: \"Operation '{{path}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  taylor-morrison-operation-description-exists:\n    description: All\
  \ operations must have a description\n    message: \"Operation '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  taylor-morrison-responses-success:\n    description: All operations must define a success response\n    message: \"Operation '{{path}}' must define a 200 or 201 response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  taylor-morrison-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  taylor-morrison-parameters-description:\n    description:\
  \ All parameters must have descriptions\n    message: \"Parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  taylor-morrison-info-contact:\n    description: API must include contact info\n    message: \"API info must include contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/taylor-morrison-home/refs/heads/main/rules/taylor-morrison-spectral-rules.yml
tags:
- Homebuilding
- Real Estate
- Fortune 1000
- New Homes
- Communities
- Mortgage
- Spectral
- Linting
- API Governance
---
