---
api_specs:
- filename: western-digital-my-cloud-home-openapi.yml
  format: yaml
  label: WD My Cloud Home API
  slug: my-cloud-home
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/western-digital/refs/heads/main/openapi/western-digital-my-cloud-home-openapi.yml
categories:
- wd
description: Spectral linting rules defining API design standards and conventions for western-digital.
layout: rules
name: western-digital API Rules
provider_name: western-digital
provider_slug: western-digital
rule_count: 7
rules:
- description: Operation IDs must use camelCase.
  given: $.paths.*.*.operationId
  name: wd-operation-id-kebab-case
  severity: warn
- description: All paths should include a version prefix (e.g. /v1/, /v2/, /sdk/v2/).
  given: $.paths[*]~
  name: wd-path-version-prefix
  severity: warn
- description: All device-tier paths must declare bearerAuth security.
  given: $.paths[?(!(/authorize|/oauth|/config))].*.security
  name: wd-bearer-auth-required
  severity: warn
- description: Successful responses should return application/json.
  given: $.paths.*.*.responses.200.content
  name: wd-response-200-content-type
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths[*]~
  name: wd-no-trailing-slash
  severity: error
- description: Each operation must include at least one tag.
  given: $.paths.*.*.tags
  name: wd-tags-defined
  severity: warn
- description: Each operation must have a description.
  given: $.paths.*.*.description
  name: wd-description-required
  severity: warn
rules_file: rules/western-digital-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/western-digital/refs/heads/main/rules/western-digital-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 6
slug: western-digital-rules
source_filename: western-digital-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  wd-operation-id-kebab-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  wd-path-version-prefix:\n    description: All paths should include a version prefix (e.g. /v1/, /v2/, /sdk/v2/).\n    message: \"Path '{{path}}' should include a version prefix (/v1/, /v2/, /sdk/v2/).\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(v[0-9]+|sdk/v[0-9]+|authservice/v[0-9]+|device/v[0-9]+|config/v[0-9]+)/\"\n\n  wd-bearer-auth-required:\n    description: All device-tier paths must declare bearerAuth security.\n    message: \"Operation '{{path}}' must include bearerAuth security.\"\n    severity: warn\n    given: \"$.paths[?(!(/authorize|/oauth|/config))].*.security\"\
  \n    then:\n      function: truthy\n\n  wd-response-200-content-type:\n    description: Successful responses should return application/json.\n    message: \"Response 200 at '{{path}}' should define application/json content.\"\n    severity: warn\n    given: \"$.paths.*.*.responses.200.content\"\n    then:\n      function: truthy\n\n  wd-no-trailing-slash:\n    description: Paths must not have a trailing slash.\n    message: \"Path '{{value}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  wd-tags-defined:\n    description: Each operation must include at least one tag.\n    message: \"Operation at '{{path}}' must include at least one tag.\"\n    severity: warn\n    given: \"$.paths.*.*.tags\"\n    then:\n      function: truthy\n\n  wd-description-required:\n    description: Each operation must have a description.\n    message: \"Operation at '{{path}}' is missing\
  \ a description.\"\n    severity: warn\n    given: \"$.paths.*.*.description\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/western-digital/refs/heads/main/rules/western-digital-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
