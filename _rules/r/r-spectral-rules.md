---
api_specs:
- filename: r-metacran-crandb-openapi.yml
  format: yaml
  label: METACRAN CranDB API
  slug: metacran-crandb
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/r/refs/heads/main/openapi/r-metacran-crandb-openapi.yml
- filename: r-metacran-cranlogs-openapi.yml
  format: yaml
  label: METACRAN CranLogs API
  slug: metacran-cranlogs
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/r/refs/heads/main/openapi/r-metacran-cranlogs-openapi.yml
- filename: r-rversions-openapi.yml
  format: yaml
  label: R Versions API
  slug: rversions
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/r/refs/heads/main/openapi/r-rversions-openapi.yml
categories:
- r
description: Spectral linting rules defining API design standards and conventions for R.
layout: rules
name: R API Rules
provider_name: R
provider_slug: r
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: r-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: r-tags-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: r-operation-ids-must-be-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: r-paths-kebab-case
  severity: warn
- description: All operations must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: r-responses-must-include-success
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: r-parameters-must-have-descriptions
  severity: warn
- description: Schema component names must use PascalCase
  given: $.components.schemas[*]~
  name: r-components-schemas-pascal-case
  severity: warn
rules_file: rules/r-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/r/refs/heads/main/rules/r-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 6
slug: r-spectral-rules
source_filename: r-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  r-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  r-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  r-operation-ids-must-be-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\
  \n\n  r-paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment must use kebab-case (no underscores or uppercase)\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z_]\"\n\n  r-responses-must-include-success:\n    description: All operations must define at least one 2xx response\n    message: \"Operation must define a 2xx success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  r-parameters-must-have-descriptions:\n    description: All parameters must have descriptions\n    message: \"Parameter '{{value}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  r-components-schemas-pascal-case:\n\
  \    description: Schema component names must use PascalCase\n    message: \"Schema name '{{value}}' must use PascalCase\"\n    severity: warn\n    given: \"$.components.schemas[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/r/refs/heads/main/rules/r-spectral-rules.yml
tags:
- R
- Statistics
- Data Science
- Open Source
- Programming Language
- Spectral
- Linting
- API Governance
---
