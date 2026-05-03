---
api_specs:
- filename: redfin-stingray-api-openapi.yml
  format: yaml
  label: Redfin Stingray API
  slug: redfin-stingray-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/redfin/refs/heads/main/openapi/redfin-stingray-api-openapi.yml
- filename: redfin-gis-csv-api-openapi.yml
  format: yaml
  label: Redfin GIS CSV Export API
  slug: redfin-gis-csv-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/redfin/refs/heads/main/openapi/redfin-gis-csv-api-openapi.yml
- filename: redfin-data-center-openapi.yml
  format: yaml
  label: Redfin Data Center
  slug: redfin-data-center
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/redfin/refs/heads/main/openapi/redfin-data-center-openapi.yml
categories:
- redfin
description: Spectral linting rules defining API design standards and conventions for Redfin.
layout: rules
name: Redfin API Rules
provider_name: Redfin
provider_slug: redfin
rule_count: 10
rules:
- description: All operationIds must use camelCase naming convention consistent with Redfin API style.
  given: $.paths[*][*].operationId
  name: redfin-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: redfin-tags-title-case
  severity: warn
- description: Operation tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: redfin-path-tags-title-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: redfin-operations-have-summaries
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][*]
  name: redfin-operations-have-descriptions
  severity: info
- description: All operations must have an operationId for SDK generation.
  given: $.paths[*][*]
  name: redfin-operations-have-operation-ids
  severity: error
- description: All response objects must have a description.
  given: $.paths[*][*].responses[*]
  name: redfin-responses-have-descriptions
  severity: warn
- description: All parameters should have descriptions.
  given: $.paths[*][*].parameters[*]
  name: redfin-parameters-have-descriptions
  severity: info
- description: API info must include contact information.
  given: $.info
  name: redfin-info-contact
  severity: warn
- description: API must have at least one server defined.
  given: $
  name: redfin-servers-defined
  severity: error
rules_file: rules/redfin-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/redfin/refs/heads/main/rules/redfin-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 6
slug: redfin-rules
source_filename: redfin-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  redfin-operation-ids-camel-case:\n    description: All operationIds must use camelCase naming convention consistent with Redfin API style.\n    message: \"OperationId '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  redfin-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /-]*$\"\n\n  redfin-path-tags-title-case:\n    description: Operation tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /-]*$\"\n\n  redfin-operations-have-summaries:\n\
  \    description: All operations must have a summary.\n    message: \"Operation at {{path}} is missing a summary.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  redfin-operations-have-descriptions:\n    description: All operations must have a description.\n    message: \"Operation at {{path}} is missing a description.\"\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  redfin-operations-have-operation-ids:\n    description: All operations must have an operationId for SDK generation.\n    message: \"Operation at {{path}} is missing an operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  redfin-responses-have-descriptions:\n    description: All response objects must have a description.\n    message: \"Response at {{path}} is missing a description.\"\n    severity: warn\n    given:\
  \ \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  redfin-parameters-have-descriptions:\n    description: All parameters should have descriptions.\n    message: \"Parameter at {{path}} is missing a description.\"\n    severity: info\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  redfin-info-contact:\n    description: API info must include contact information.\n    message: \"API info is missing a contact block.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  redfin-servers-defined:\n    description: API must have at least one server defined.\n    message: \"API is missing a servers block.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/redfin/refs/heads/main/rules/redfin-rules.yml
tags:
- CSV Export
- GIS
- Home Values
- Housing Market
- Listings
- Property Data
- Real Estate
- Spectral
- Linting
- API Governance
---
