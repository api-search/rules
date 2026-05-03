---
api_specs:
- filename: taxi-language-openapi.yml
  format: yaml
  label: Taxi Language
  slug: taxi-language
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/taxi-describe-how-your-apis-and-data-relate/refs/heads/main/openapi/taxi-language-openapi.yml
categories:
- taxi
description: Spectral linting rules defining API design standards and conventions for Taxi - Describe How Your APIs and Data Relate.
layout: rules
name: Taxi - Describe How Your APIs and Data Relate API Rules
provider_name: Taxi - Describe How Your APIs and Data Relate
provider_slug: taxi-describe-how-your-apis-and-data-relate
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: taxi-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: taxi-path-kebab-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: taxi-operation-summary-exists
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: taxi-operation-description-exists
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: taxi-response-200-exists
  severity: error
- description: Tags must use Title Case
  given: $.tags[*].name
  name: taxi-tags-title-case
  severity: warn
- description: API must include license information (open source)
  given: $.info
  name: taxi-info-license
  severity: warn
- description: Component schemas must have descriptions
  given: $.components.schemas[*]
  name: taxi-schema-descriptions
  severity: warn
rules_file: rules/taxi-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/taxi-describe-how-your-apis-and-data-relate/refs/heads/main/rules/taxi-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: taxi-spectral-rules
source_filename: taxi-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  taxi-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  taxi-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment must use kebab-case: {{path}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*$\"\n\n  taxi-operation-summary-exists:\n    description: All operations must have a summary\n    message: \"Operation at '{{path}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  taxi-operation-description-exists:\n    description: All operations must have a description\n   \
  \ message: \"Operation at '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  taxi-response-200-exists:\n    description: All operations must define a 200 response\n    message: \"Operation at '{{path}}' must define a 200/201 success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  taxi-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  taxi-info-license:\n    description: API must include license information (open source)\n    message:\
  \ \"Open source API must include license info\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  taxi-schema-descriptions:\n    description: Component schemas must have descriptions\n    message: \"Schema '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/taxi-describe-how-your-apis-and-data-relate/refs/heads/main/rules/taxi-spectral-rules.yml
tags:
- API Description
- Data Integration
- Open Source
- Query Language
- Schema
- Semantic
- Spectral
- Linting
- API Governance
---
