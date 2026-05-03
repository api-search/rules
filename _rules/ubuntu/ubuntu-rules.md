---
api_specs:
- filename: ubuntu-launchpad-openapi.yml
  format: yaml
  label: Launchpad API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ubuntu/refs/heads/main/openapi/ubuntu-launchpad-openapi.yml
- filename: ubuntu-snap-store-openapi.yml
  format: yaml
  label: Snap Store API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ubuntu/refs/heads/main/openapi/ubuntu-snap-store-openapi.yml
- filename: ubuntu-cve-openapi.yml
  format: yaml
  label: Ubuntu CVE API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ubuntu/refs/heads/main/openapi/ubuntu-cve-openapi.yml
categories:
- ubuntu
description: Spectral linting rules defining API design standards and conventions for Ubuntu.
layout: rules
name: Ubuntu API Rules
provider_name: Ubuntu
provider_slug: ubuntu
rule_count: 6
rules:
- description: Operation IDs must use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: ubuntu-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: ubuntu-has-tags
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: ubuntu-has-operation-id
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: ubuntu-has-description
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: ubuntu-summary-title-case
  severity: warn
- description: Successful GET responses should define a content schema.
  given: $.paths[*].get.responses.200
  name: ubuntu-200-response-content
  severity: warn
rules_file: rules/ubuntu-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ubuntu/refs/heads/main/rules/ubuntu-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 5
slug: ubuntu-rules
source_filename: ubuntu-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ubuntu-operation-id-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ubuntu-has-tags:\n    description: All operations must have at least one tag.\n    message: Operation is missing tags.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  ubuntu-has-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  ubuntu-has-description:\n    description: All operations must have a description.\n    message:\
  \ Operation is missing a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  ubuntu-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  ubuntu-200-response-content:\n    description: Successful GET responses should define a content schema.\n    message: GET 200 response at '{{path}}' should define content.\n    severity: warn\n    given: \"$.paths[*].get.responses.200\"\n    then:\n      field: content\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ubuntu/refs/heads/main/rules/ubuntu-rules.yml
tags:
- Cloud
- Containers
- Devops
- Enterprise
- Linux
- Security
- Ubuntu
- Package Management
- Open Source
- Spectral
- Linting
- API Governance
---
