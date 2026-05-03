---
api_specs:
- filename: rapidoc-rapidoc-openapi.yml
  format: yaml
  label: RapiDoc
  slug: rapidoc
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidoc/refs/heads/main/openapi/rapidoc-rapidoc-openapi.yml
categories:
- rapidoc
description: Spectral linting rules defining API design standards and conventions for RapiDoc.
layout: rules
name: RapiDoc API Rules
provider_name: RapiDoc
provider_slug: rapidoc
rule_count: 5
rules:
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: rapidoc-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: rapidoc-tags-title-case
  severity: warn
- description: All operations should have a summary.
  given: $.paths[*][*]
  name: rapidoc-operations-have-summaries
  severity: warn
- description: API info version should follow semantic versioning.
  given: $.info.version
  name: rapidoc-info-version-semver
  severity: hint
- description: GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: rapidoc-response-200-for-get
  severity: error
rules_file: rules/rapidoc-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rapidoc/refs/heads/main/rules/rapidoc-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 3
slug: rapidoc-rules
source_filename: rapidoc-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rapidoc-operation-ids-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rapidoc-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]*$\"\n\n  rapidoc-operations-have-summaries:\n    description: All operations should have a summary.\n    message: \"Operation at '{{path}}' should have a summary.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  rapidoc-info-version-semver:\n    description: API info version should follow semantic\
  \ versioning.\n    message: \"API version '{{value}}' should follow semver format (e.g., 9.3.4).\"\n    severity: hint\n    given: \"$.info.version\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[0-9]+\\\\.[0-9]+\\\\.[0-9]\"\n\n  rapidoc-response-200-for-get:\n    description: GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: 200\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rapidoc/refs/heads/main/rules/rapidoc-rules.yml
tags:
- Documentation
- Platform
- Web Components
- OpenAPI
- Spectral
- Linting
- API Governance
---
