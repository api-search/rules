---
api_specs:
- filename: ssh-key-management-openapi.yml
  format: yaml
  label: OpenSSH Key Management API
  slug: openssh-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ssh/refs/heads/main/openapi/ssh-key-management-openapi.yml
categories:
- ssh
description: Spectral linting rules defining API design standards and conventions for SSH.
layout: rules
name: SSH API Rules
provider_name: SSH
provider_slug: ssh
rule_count: 6
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ssh-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: ssh-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: ssh-tags-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][*].description
  name: ssh-description-required
  severity: warn
- description: All key management operations must require authentication
  given: $.paths[*/keys*][*]
  name: ssh-key-operations-security
  severity: error
- description: All operations must define a success response
  given: $.paths[*][get,post,put,delete]
  name: ssh-response-success-required
  severity: error
rules_file: rules/ssh-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ssh/refs/heads/main/rules/ssh-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 3
slug: ssh-rules
source_filename: ssh-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ssh-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s?)+$\"\n\n  ssh-operationid-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ssh-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  ssh-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  ssh-key-operations-security:\n    description: All key management operations\
  \ must require authentication\n    severity: error\n    given: \"$.paths[*/keys*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  ssh-response-success-required:\n    description: All operations must define a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: responses\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ssh/refs/heads/main/rules/ssh-rules.yml
tags:
- SSH
- Secure Shell
- Remote Access
- Cryptography
- Network Security
- System Administration
- Spectral
- Linting
- API Governance
---
